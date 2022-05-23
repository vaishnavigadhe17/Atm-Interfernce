
 /*import java.time.LocalDate;             //Importing Packages
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Scanner;*/

class Main {

    public static void main(String[] args) {  
        
    
// import java.time.LocalDate;             //Importing Packages
//import java.time.LocalTime;
//import java.time.format.DateTimeFormatter;
//import java.util.ArrayList;
//import java.util.Scanner;//



  //Main Method. The execution starts from this method
	{
		
		String accname = "Soham Chotalia";    //Declaring the account details
		String branchname = "Borivali (west)";
		String branchaddress = "C-002, Vasundra Apartment, SV Road, Borivali (west), Mumbai";
		String branchIFSC = "OBC287945";
		
		int accnumber = 29873679;
		int password = 1707;
		int balance = 100;
		int minbal = 5000;
		boolean flag = true;
		boolean flagb = true;
		boolean flagc = true;
		int paper = 0;
		int attempt = 5;
		int currattempt = 0;
		
		LocalDate tarik = LocalDate.now();  // Declaring the date format
		String dateStr = tarik.format(DateTimeFormatter.ofPattern("dd-MMM-yyyy"));
		
		LocalTime dt = LocalTime.now();    // Declaring the time format
		String timeStr = dt.format(DateTimeFormatter.ofPattern("hh:mm:ss a"));
		
		ArrayList<String> trans = new ArrayList<String>();     // Declaring a new array
		
		Scanner sc = new Scanner(System.in);                // Importing the scanner class
		
		while(currattempt<attempt)               // Limiting the number of attempts for entering correct password
		{
			System.out.println("Enter your pin");
			int pass = sc.nextInt();
			if(pass==password)                // Checking if entered pin is same as the acccount pin
			{
				System.out.println("Do you want paper receipt");   // Asking if user wants to print receipt
				System.out.println("1. Yes");
				System.out.println("2. No");
				paper = sc.nextInt();
				break;
			}
			else
				System.out.println("You have entered wrong pin");
			currattempt = currattempt + 1;
		}
		
		
		if(currattempt<5)     // Executing the main task if users enters correct password within limited attempts
		{
			while(flag==true)
			{
				System.out.println("****");
				System.out.println("1. Transaction History");
				System.out.println("2. Withdraw");
				System.out.println("3. Deposit");
				System.out.println("4. Transfer");
				System.out.println("5. Quit");
				System.out.println("6. Change Password");
				
				System.out.println("What would to like to do today");
				int option = sc.nextInt();
				
				switch(option)
				{
					case 1:       // Option for transaction history
					{	
						System.out.println("Your Transaction History");
						for(String q: trans)
						{
							System.out.println(q);
						}
						break;
					}
					
					
					
					case 2:     // Option for withdrawl
					{
						while(true)
						{
							System.out.println("Enter the withdrawl amount");
							int withdraw = sc.nextInt();
							if((withdraw % 10) ==0)
							{
								if(withdraw <= balance)
								{
									if((balance - withdraw) <1000)
									{
										System.out.println("Minimum balance has to Rs 1000");
									}
									else
									{
										balance = balance - withdraw;
										String sf2 = String.format("You have successfully withdrawl Rs %d",withdraw);
										String sf3 = String.format("Your balance is Rs %d", balance);
										System.out.println(sf2);
										System.out.println(sf3);
										
										String wt = String.format("Withdrawl - Rs %d", withdraw);
										trans.add(wt);
										break;
									}
									
								}
								else
								{
									System.out.println("Insufficient balance");
								}
							}
							else
								System.out.println("Enter the withdraw amount in multiples of 100");
						}
						
						
						break;
					}
					
					
					
					case 3:           // Option for deposit
					{
						while(true)
						{
							System.out.println("Enter the deposit amount");
							int deposit = sc.nextInt();
							if((deposit%10)==0)
							{
								balance = balance + deposit;
								String sf1 = String.format("You have successfully deposited Rs %d", deposit);
								String sf4 = String.format("Your balance is Rs %d", balance);
								System.out.println(sf1);
								System.out.println(sf4);
								
								String dp = String.format("Deposit - Rs %d", deposit);
								trans.add(dp);
								
								break;
							}
							else
							{
								System.out.println("Enter the amount in multiples of 100");
							}
						}
						
						break;
					}
					
					
					
					case 4:      // Option for transfer
					{
						while(true)
						{
							System.out.println("Enter the accout number of the beneficiary");
							int accno = sc.nextInt();
							System.out.println("Enter the IFSC code of the bank of the beneficiary");
							String ifsc = sc.next();
							System.out.println(accno);
							System.out.println("Please confirm the account number of the beneficiary");
							System.out.println("1. Correct");
							System.out.println("2. Incorrect");
							int conf = sc.nextInt();
							if(conf==1)
							{
								System.out.println("Enter the amount you want to transfer");
								int transfamount = sc.nextInt();
								if((transfamount % 10) ==0)
								{
									if(transfamount <= balance)
									{
										if((balance - transfamount) <1000)
										{
											System.out.println("Minimum balance has to Rs 1000");
										}
										else
										{
											balance = balance - transfamount;
											String sf2 = String.format("You have successfully transfered Rs %d to %d",transfamount,accno);
											String sf3 = String.format("Your balance is Rs %d", balance);
											System.out.println(sf2);
											System.out.println(sf3);
											
											String tf = String.format("Transfer - Rs %d", transfamount);
											trans.add(tf);
											break;
										}
										
									}
									else
									{
										System.out.println("Insufficient balance");
									}
								}
								else
									System.out.println("Enter the amount in multiple of 100");
							}
							else
								System.out.println("You entered incorrect account number");
						}
						
						break;
					}
					
					
					
					case 5:          // Option to end 
					{
						System.out.println("Thank you for banking with us");
						flag = false;
						break;
					}
					
					
					case 6:          // Option for changing pin
					{
						System.out.println("Enter your new pin");
						int newpin = sc.nextInt();
						password = newpin;
						System.out.println("Do not share your pin with anyone");
						System.out.println("You have successfully changed your password");
						trans.add("Changed Password");
					}
					
					
					default:
						System.out.println("Please select an appropriate option");
						break;
				}
				
				System.out.println("Would you like to do another transaction");
				System.out.println("1. Yes");
				System.out.println("2. No");
				int df = sc.nextInt();
				if(df==1)
					flag = true;
				else
					flag = false;
						
			}
			if(paper==1)
			{
				String sf6 = String.format("Date: %s", dateStr);       // Printing the receipt
				String sf7 = String.format("Time: %s", timeStr);
				//String sf8 = String.format("%s     %s", LocalDate.now().toString(), LocalTime.now().toString());
				String sf9 = String.format("Account Holder Name: %s", accname);
				String sf10 = String.format("Branch Name: %s", branchname);
				String sf11 = String.format("Branch Address: %s", branchaddress);
				String sf12 = String.format("Branch IFSC code: %s", branchIFSC);
				String sf13 = String.format("Account Number: %d", accnumber);
				String sf14 = String.format("Your account balance is Rs %d", balance);
				System.out.println(sf6);
				System.out.println(sf7);
				System.out.println(sf9);
				System.out.println(sf10);
				System.out.println(sf11);
				System.out.println(sf12);
				System.out.println(sf13);
				System.out.println(sf14);
				
			}
			System.out.println("Thank you for banking with us");
		}
		else
		{
			System.out.println("You have entered wrong pin multiple times");
		}

	}


      
    }
}
