######  Introduction ############
# Name : Junaid Masood			#
# reg : CS151025				#
# Course : Assembly Language	#
# Final Project					#
# Restaurant Bill Generator		#
#################################



.data
  #### Menu Messages ######
	welcomeMsg 		  : .asciiz "Welcome To Junaid's Restaurant\nplease Select the food\n"
    Dishes    		  : .asciiz "\n\n1.Continental\n2.Pakistani\n3.Indian\n4.Irani\n5.Chinese\n6.Generate The bill\n\n"		
	Total			  : .asciiz "\nTotal : "
  
  #### Continental Dishes####
	ContinentalDishes : .asciiz "1.Roast Chicken\t\t250 \n2.Grilled Chicken\t\t270\n3.Irish Chicken Bangers\t150\n4.Garlic Prawn Risotto\t\t100\n5.Vegetable Au Gratin\t\t140\n6.To go back\n"
	Roast             : .asciiz "\nRoast Chicken\t\t250" 
	grilled			  : .asciiz "\nGrilled Chicken\t\t270"
	irish             : .asciiz "\nIrish Chicken Bangers\t\t150"
	garlic            : .asciiz "\nGarlic Prawn Risotto\t\t100"
	vegetable         : .asciiz "\nVegetable Au Gratin\t\t140"
  
  #### pakistani Dishes####
	PakistaniDishes  : .asciiz "1.Biryani\t\t120\n2.Qorma\t\t70\n3.pilao\t\t90\n4.Yakhni\t\t50\n5.Kaali Daal\t30\n6.To go back\n"
	biryani 		 : .asciiz "\nBriyani"
	qorma 			 : .asciiz "\nQorma"
	pilao            : .asciiz "\npilao"
	daal             : .asciiz "\nDaal"
	yakhni           : .asciiz "\nYakhni"
  
  #### Indian Dishes####
	IndianDishes  	 : .asciiz  "1.Sajjige\t\t55\n2.Sambar\t\t70\n3.Sevai\t\t110\n4.Bhatura\t\t90\n5.Baati\t\t150\n6.To go back\n"
    Sajjige			 : .asciiz  "\nSajjige"
	Sambar			 : .asciiz	"\nSambar"
	Sevai  			 : .asciiz  "\nSevai"
	Bhatura			 : .asciiz  "\nBhatura"
	Baati			 : .asciiz  "\nBaati"
	
  #### Chinese Dishes ####
	ChineseDishes    : .asciiz  "1.Wonton\t\t15\n2.Dumpling\t\t60\n3.Chow Mein\t\t80\n4.Fried Rice\t65\n5.Noodle\t\t40\n6.To go back\n"	
    Wontons			 : .asciiz  "\nWontons"
    Dumplings		 : .asciiz	"\nDumplings"
    ChowMein         : .asciiz	"\nChow Mein"
    FriedRice        : .asciiz	"\nFried Rice"
    Noodle           : .asciiz	"\nNoodle"

  #### drinks ####
	drink			 : .asciiz "1.cold Drink\t30\n2.Lassi\t\t35\n3.Lemonade\t\t40\n4.Doodh Soda\t60\n5.Tea\t\t20"
	coldDrink 		 : .asciiz "\nCold Drink"
	lassi 			 : .asciiz "\nLassi"
	lemonade 		 : .asciiz "\nLemonade"
	doodhSoda 		 : .asciiz "\nDoodh Soda"
	tea 			 : .asciiz "\nTea"
	
  #### file address #####	
    file 			 : .asciiz "G:\DHA Suffa\Semester 3\Coal\proejct\record.txt" 
    dish : .word 0
	
	
  ### Reading Varaibles ####
	inputVariable 	 : .space 1024

.text
.globl main
main:
			
			 	
		########to opening the file############
 	
		la $a0,file  # address of file in the a0
		li $a1,1     # a1=  1 to write in the file
		li $a2 , 0   #dont know what is this for
		li $v0,13    # to open the file
		syscall
		move $t6,$v0
		########################################

	li $t5,0 			# t5 = 0 it will count the total
	li $t7,0 			# t7 = 0 because it is the loop variable
################################
	la $a0,welcomeMsg 	 
	li $v0,4			# printing The Welcome message
	syscall
################################
	
	loop:				
	beq $t7,1,exit		# loop Starts here
										#|
###############################			#|
	la $a0,Dishes 						#|
	li $v0,4			# showing the menu of dishes
	syscall								#|
################################		#|
	li $v0,5			# taking input to choose the dish
	syscall				# dish = any number(1,2,3,4,5)
	sw $v0,dish			# dish is the data type word for to contain the value input by the user to select menu		
################################		#|					
	lw $t0,dish			# t0 = dish
	beq $t0,1,Continental		# if(t0 == 1) { Jump to continental  }
	cont:								#|									
###############################			#|
	beq $t0,2,Pakistani		# if(t0 == 2) { Jump to pakistani  }
	pak:								#|							
###############################			#|						
	beq $t0,3,Indian		# if(t0 == 3) { Jump to India  }
	ind:								#|										
###############################			#|								#|									
	beq $t0,4,DrinkStuff			# if(t0 == 4) { Jump to Irani  }
	drinks:								#|								
###############################			#|
	beq $t0,5,Chinese		# if(t0 == 5) { Jump to Chinese  }
	china:								#|								
###############################	
	beq $t0,6,GeneratingBill 	# if(t0 == 6) { Jump to Generating Bill }
	Bill:								#|				
##############################			#|
	j loop			# loop end here
	exit:

	######close the file#####
 	#li $v0,16
 	#move $a0,$t2
 	#syscall
	#########################
	
	la $a0,inputVariable
	li $v0,4
	syscall
	
	la $a0,Total
	li $v0,4
	syscall
	
	move $a0,$t5
	li $v0,1
	syscall
 	
 li $v0 10
 syscall
 

 
 	#Funtions part 
 ####################################################################################################
 
Continental:
 
	 la $a0,ContinentalDishes
 	 li $v0,4			# priting the menu of Cont dishes
 	 syscall
  	##########
  	li $t1,0
  	##########
  	loopC:				# loop for taking input or order dishes
     	beq $t1,6,exitC			# when press 6 loop will terminate
	#######  
	  li $v0,5			# taking input
	  syscall
  	
  	  move $t1,$v0			# ti = input
  	  beq $t1,1,ConBill1
  	  beq $t1,2,ConBill2
  	  beq $t1,3,ConBill3
	  beq $t1,4,ConBill4	
      beq $t1,5,ConBill5
  	
  	 conBillr1:		
  	#######
  				
	  j loopC
 	 exitC:
  
  
 j cont
 #####################################################################################################
 
Pakistani:
 
	 la $a0,PakistaniDishes
 	 li $v0,4			# priting the menu of Cont dishes
 	 syscall
  	##########
  	li $t1,0
  	##########
  	loopP:				# loop for taking input or order dishes
     	beq $t1,6,exitP			# when press 6 loop will terminate
	#######  
	  li $v0,5			# taking input
	  syscall
	  
	  move $t1,$v0			# ti = input
  	  beq $t1,1,pakBill1
  	  beq $t1,2,pakBill2
  	  beq $t1,3,pakBill3
	  beq $t1,4,pakBill4	
      beq $t1,5,pakBill5
  	
  	 pakBillr1:					
	  j loopP
 	 exitP:
  
  
 j pak
 ###############################################################################################
 
 #####################################################################################################
 
Indian:
 
	 la $a0,IndianDishes
 	 li $v0,4			# priting the menu of Cont dishes
 	 syscall
  	##########
  	li $t1,0
  	##########
  	loopI:				# loop for taking input or order dishes
     	beq $t1,6,exitI			# when press 6 loop will terminate
	#######  
	  li $v0,5			# taking input
	  syscall
  	  move $t1,$v0			# ti = input
  	  beq $t1,1,indBill1
  	  beq $t1,2,indBill2
  	  beq $t1,3,indBill3
	  beq $t1,4,indBill4	
      beq $t1,5,indBill5
  	
  	 indBillr1:							
	  j loopI
 	 exitI:
  
  
 j ind
 ############################################################################################

  
DrinkStuff:
 
	 la $a0,drink
 	 li $v0,4			# priting the menu of Cont dishes
 	 syscall
  	##########
  	li $t1,0
  	##########
  	loopd:				# loop for taking input or order dishes
     	beq $t1,6,exitd			# when press 6 loop will terminate
	#######  
	  li $v0,5			# taking input
	  syscall
	  move $t1,$v0			# ti = input
  	  beq $t1,1,dBill1
  	  beq $t1,2,dBill2
  	  beq $t1,3,dBill3
	  beq $t1,4,dBill4	
      beq $t1,5,dBill5
  	
  	 dBillr1:			
	  j loopd
 	 exitd:
  
  
 j drinks
 ############################################################################################
 
   
Chinese:
 
	 la $a0,ChineseDishes
 	 li $v0,4			# priting the menu of Cont dishes
 	 syscall
  	##########
  	li $t1,0
  	##########
  	loopCh:				# loop for taking input or order dishes
     	beq $t1,6,exitCh			# when press 6 loop will terminate
	#######  
	  li $v0,5			# taking input
	  syscall
	  move $t1,$v0			# ti = input
  	  beq $t1,1,chiBill1
  	  beq $t1,2,chiBill2
  	  beq $t1,3,chiBill3
	  beq $t1,4,chiBill4	
      beq $t1,5,chiBill5
  	
  	 chiBillr1:					
	  j loopCh
 	 exitCh:
  
  
 j china
 ############################################################################################
   
       GeneratingBill:
		
			li $v0,16     # closing the writting file
			move $a0, $t6
			syscall 
			########opening file for reading ########
				
				la $a0 , file
				li $a1,0
				li $a2,0
				li $v0,13
				syscall
				
				move $t6,$v0
				
				####Now Read Fromt the file ####
				li $v0,14
				move $a0,$t6
				
				la $a1,inputVariable
				li $a2,100000
				syscall
				
				li $v0,16
				move $a0,$t6
				syscall
			##########################################
			li $t7 ,1 # for exiting to the program
 j Bill
 
 
 
 ########################################################
 
 ##########################################Continental Billing part ##############################
 #bill part
 

 ConBill1:
 	
	
	move $t2,$t6 				# my object is in $v0 so transfering it into 
 	#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Roast
 	li $a2,11
 	syscall
 
	addi $t5,$t5,250
 	
 
 j conBillr1
 
 ###################
 ConBill2:
	
	
	move $t2,$t6 # my object is in $v0 so transfering it into 
 	#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,grilled
 	li $a2,8
 	syscall
 	
	addi $t5,$t5,270
 
 j conBillr1
 
 ###################

  ConBill3:
	
	
	move $t2,$t6 # my object is in $v0 so transfering it into 
 	#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,irish
 	li $a2,7
 	syscall
 	
	addi $t5,$t5,150
    
 j conBillr1
 
 ###################
 
  ConBill4:
	
	
	move $t2,$t6 # my object is in $v0 so transfering it into 
 	#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,garlic
 	li $a2,7
 	syscall
 	
	addi $t5,$t5,100
 
 j conBillr1
 
 ###################
 
  ConBill5:
	
	
	move $t2,$t6 # my object is in $v0 so transfering it into 
 	#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,vegetable
 	li $a2,10
 	syscall
 	
	addi $t5,$t5,140
 
 j conBillr1
 
########################################## Continental Billing part Ending ##############################################################

##########################################Pakistani Billing part #######################################################################
pakBill1:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,biryani
 	li $a2,8
 	syscall
	
	addi $t5,$t5,120

j pakBillr1

###########################

pakBill2:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,qorma
 	li $a2,6
 	syscall
	
	addi $t5,$t5,70
j pakBillr1

###########################

pakBill3:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,pilao
 	li $a2,7
 	syscall
	
	addi $t5,$t5,90
j pakBillr1


###########################

pakBill4:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,yakhni
 	li $a2,7
 	syscall
	
	addi $t5,$t5,50
j pakBillr1


###########################

pakBill5:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,daal
 	li $a2,5
 	syscall
	
	addi $t5,$t5,30
j pakBillr1


##########################################pakistani Billing part #########################################################################

##########################################Indian Billing part #########################################################################

indBill1:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Sajjige
 	li $a2,8
 	syscall
	
	addi $t5,$t5,55
j indBillr1


########################

indBill2:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Sambar	
 	li $a2,7
 	syscall
	
	addi $t5,$t5,70
j indBillr1


########################

indBill3:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Sevai
 	li $a2,6
 	syscall
	
	addi $t5,$t5,110
j indBillr1


########################

indBill4:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Bhatura
 	li $a2,8
 	syscall
	
	addi $t5,$t5,90
j indBillr1

########################

indBill5:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Baati
 	li $a2,6
 	syscall
	
	addi $t5,$t5,150
j indBillr1


##########################################Indian Billing part #########################################################################



########################################## Chinese Billing part #########################################################################

chiBill1:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Wontons
 	li $a2,8
 	syscall
	
	addi $t5,$t5,15

j chiBillr1

########################

chiBill2:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Dumplings	
 	li $a2,10
 	syscall
	
	addi $t5,$t5,60
j chiBillr1


########################

chiBill3:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,ChowMein
 	li $a2,10
 	syscall
	
	addi $t5,$t5,80
j chiBillr1


########################

chiBill4:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,FriedRice
 	li $a2,11
 	syscall
	
	addi $t5,$t5,65
j chiBillr1

########################

chiBill5:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,Noodle
 	li $a2,7
 	syscall
	
	addi $t5,$t5,40
j chiBillr1

########################################## chinese Billing part #########################################################################



########################################## drinks Billing part #########################################################################

dBill1:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,coldDrink
 	li $a2,11
 	syscall
	
	addi $t5,$t5,30

j dBillr1

#######################

dBill2:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,lassi	
 	li $a2,6
 	syscall
	
	addi $t5,$t5,35

j dBillr1


########################

dBill3:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,lemonade
 	li $a2,9
 	syscall
	
	addi $t5,$t5,40
j dBillr1


########################

dBill4:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,doodhSoda
 	li $a2,11
 	syscall
	
	addi $t5,$t5,60
j dBillr1

########################

dBill5:

	move $t2,$t6 				# my object is in $v0 so transfering it into 
								#to write in the file
 	li $v0,15   
 	move $a0,$t2
 	la $a1,tea
 	li $a2,4
 	syscall
	
	addi $t5,$t5,20
j dBillr1
	 		

########################################## drinks Billing part #########################################################################
