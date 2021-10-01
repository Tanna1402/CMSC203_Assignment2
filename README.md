# CMSC203_Assignment2
import java.util.Random;
import java.util.Scanner;

import java.util.Scanner;
public class RandomNumberGuesser{
	private static int count=0;
	static Scanner scan;
	public RandomNumberGuesser() {
		count++;
	}
	
	/**
	 * Sets the count to zero
	 */
	public static void resetCount() {
		count = 0;
	}
	
	/**
	 * generates a random integer between 1 and 100
	 * @return the random number as an integer
	 */
	public static int rand() {
		Random rand = new Random();
		int randInt = rand.nextInt(100)+1;
		return randInt;
	}
	
	/**
	 * Checks that nextGuess is strictly between lowGuess and highGuess
	 * @param nextGuess
	 * @param lowGuess
	 * @param highGuess
	 * @return a boolean, true if the guess is with the bounds, false otherwise
	 */
	public static boolean inputValidation(int nextGuess, int lowGuess, int highGuess) {
		Scanner input = new Scanner(System.in);
		boolean rtnValue;
		do {
			rtnValue = true;
			if (nextGuess>=highGuess || nextGuess<=lowGuess) {
					   System.out.println("   >>> Guess must be between "+lowGuess+" and "+highGuess+
							   ".  Try again");		
					   nextGuess = input.nextInt();
					   rtnValue = false;
				   }
		} while (nextGuess>=highGuess || nextGuess<=lowGuess);
		count++;
		return rtnValue;
		
	}

	/**
	 * @return an integer, the current value of count
	 */
	public static int getCount() {
		return count;
	}
	public static void main(String[] args) {
		Scanner guess = new Scanner(System.in);
		String playAgain=" ";
		//Declare variables
		int firstGuess=-1;
		int nextGuess = 0;
		int lowGuess = 0;
		int highGuess = 100;
		int randNum;
		
		do 
		{
			
		randNum = rand();	
		//reset the count to 0
			resetCount();
			count++;
			
			
		//ask for the user's input
			System.out.println("Enter your first guess");
			firstGuess = guess.nextInt();
			
		//Validate the range of the firstGuess
			//when the input is not in the range
			if(firstGuess<0 || firstGuess>100)
			{
				System.out.println("Your guess should be between 0 and 100. Please try again!");
				System.out.println("Enter your guess");
				firstGuess = guess.nextInt();
			}
			//when the input is in the range
			else 
			{
				do
				{
				//Count the number of guess
					System.out.println("Number of guesses is " + getCount());
					
				//Compare the firstGuess to the randNum
					//when the firstGuess equals to the randNum
					if(firstGuess==randNum)
					{
						System.out.println("Congratulations, you guessed correctly");
						System.out.println("Try again? (yes or no)");
						Scanner sc = new Scanner(System.in);
						playAgain = sc.nextLine();
						//if NO
						if(playAgain.equalsIgnoreCase("no"))
						{
							System.out.println("Thanks for playing...");
							System.exit(0);;
						}
						//if YES
						else if(playAgain.equalsIgnoreCase("yes"))
						{
							resetCount();
							firstGuess=0;
							nextGuess=0;
							randNum=0;
						}
					}
					//When the firstGuess does not equals to the randNum
					else if (firstGuess!=randNum)
					{
						//When larger
						if(firstGuess>randNum)
						{
							highGuess = firstGuess;
							System.out.println("Your guess is too high");
							System.out.println("Enter your guess between " + lowGuess + " and " +  firstGuess);
							firstGuess = guess.nextInt();
							nextGuess=firstGuess;
							if (nextGuess>=firstGuess || nextGuess<=lowGuess)
							{
								inputValidation(nextGuess,lowGuess,highGuess);
								
							}
						}
						//When smaller
						else if(firstGuess<randNum)
						{
							lowGuess = firstGuess;
							System.out.println("Your guess is too low");
							System.out.println("Enter your guess between " + firstGuess + " and " +  highGuess);
							firstGuess = guess.nextInt();
							nextGuess=firstGuess;
							if (nextGuess>=firstGuess || nextGuess<=lowGuess)
							{
								inputValidation(nextGuess,lowGuess,highGuess);
								
							}
						}
						
					}
				}
				while(randNum!=nextGuess);
				if(count>1)
				{
					System.out.println("Congratulations, you guessed correctly");
					System.out.println("Try again? (yes or no)");
					Scanner sc = new Scanner(System.in);
					playAgain = sc.nextLine();
					
						//if NO
						if(playAgain.equalsIgnoreCase("no"))
						{
							System.out.println("Thanks for playing...");
						}
				}
			}
				
		}
		while(playAgain.equalsIgnoreCase("yes"));
	}
}



