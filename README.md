    #include <iostream>
    #include <fstream>
    #include <iomanip>
    using namespace std;

    void ReadInput(ifstream &, int [], float [], int&);
    void PrintArray(ofstream &, int [], float [], int&);
    void PrintScoreA(ofstream &, int [], float [], int&);
    void PrintScoreB(ofstream &, int [], float [], int&);
    void PrintScoreC(ofstream &, int [], float [], int&);
    void PrintScoreD(ofstream &, int [], float [], int&);
    void PrintScoreF(ofstream &, int [], float [], int&);
    void FindLowScore(float [], int&, int&);
    void FindHighScore(float [], int&, int&);
    void FindAverage(float [], int&, float&);
    void Footer (ofstream &); 
    void Header (ofstream &);

    int main()
    {
    ifstream input ("DATA2.TXT", ios::in);
	ofstream output ("OUTPUT", ios::out);
	output.setf(ios:: fixed);
	output.precision(2);
	int studentIDs[50]; //creates an array with fifty integer places for student id's
	float testScores[50]; //creates an array with fifty float places for test scores
	int EU;
	float sum;
	int highScore = 0; //Initialize highScore to zero
	int lowScore = 0; //Initialize lowScore to zero

	Header(output);
	ReadInput(input,studentIDs,testScores, EU);

	output << "Student ID #"<< "  "<< "Test Score"<< endl;
	PrintArray(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	output << "Students receiving a grade of A are: ";
	PrintScoreA(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	output << "Students receiving a grade of B are: ";
	PrintScoreB(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	output << "Students receiving a grade of C are: ";
	PrintScoreC(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	output << "Students receiving a grade of D are: ";
	PrintScoreD(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	output << "Students receiving a grade of F are: ";
	PrintScoreF(output, studentIDs, testScores, EU);
	output << endl;
	output << endl;

	FindLowScore(testScores, EU, lowScore);
	output << "The lowest test score was " << testScores[lowScore] 
	<< " achieved by student " <<studentIDs[lowScore] << endl;
	output << endl;

	FindHighScore(testScores, EU, highScore);
	output <<"The highest test score was " << testScores[highScore]
	<< " achieved by student " << studentIDs[highScore] << endl;
	output << endl;
	
	FindAverage(testScores, EU, sum);
	output << "The average test score for the group is ";
	output << (sum/EU);
	output << endl;
	output << endl;
	
	Footer(output);
    }
    
    void ReadInput(ifstream &infile, int IDs[], float scores[], int &elementsUsed)
			// Recieves - the input file, array of student IDs, array of test scores, and elements used. 
			// Task - reads in the student IDs and test scores from a file
			// Returns - Nothing
    {
	  int num; 
	  float score;
	  elementsUsed = 0;
	infile>>num; //read in the first student ID
	infile>>score; //read in the first test score
	while(num > 0) //Stay in loop while the placeholder value is greater than zero
	{
		if(num < 0 || score < 0) //check to see that both inputs are greater than zero
			return;
		IDs[elementsUsed] = num; //place the first ID into the array of student IDs
		scores[elementsUsed] = score; //place the first test score into the array of test scores
		infile >>num; //read in the next ID
		infile >>score; //read in the next test score
		elementsUsed++;
	}
	return;
    }
  
    void PrintArray(ofstream &outfile, int IDs[], float scores[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints the array of student IDs and test scores in columns
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in this loop until there are no more values
	{
		outfile << setw(5) << IDs[i]<<" "; 
		outfile << setw(15)<< scores[i];
		outfile << endl;
	}
	return;
    }

    void PrintScoreA(ofstream &outfile, int ID[], float score[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints tests score that are 90.0 or greater
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in the loop until every element has been checked
	{
		if(score[i]>90.0) //print the test score if it is greater than 90.0
			outfile<<ID[i]<< " "; 
	}
	return;
    }
    
    void PrintScoreB(ofstream &outfile, int ID[], float score[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints tests score that are greater than 80.0 and less than 90.0
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in the loop until every element has been checked
	{
		if(score[i]>80.0 && score[i]<90.0) //print test score if greater than 80.0, but less than 90.0
			outfile<<ID[i]<< " "; 
	}
	 return;
    }

    void PrintScoreC(ofstream &outfile, int ID[], float score[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints tests score that are greater than 70.0 and less than 80.0
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in the loop until every element has been checked
	{
		if(score[i]>70.0 && score[i]<80.0) //print test score if greater than 70.0, but less than 80.0
			outfile<<ID[i]<< " "; 
	}
	return;
    }
    
    void PrintScoreD(ofstream &outfile, int ID[], float score[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints tests score that are greater than 60.0 and less than 70.0
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in the loop until every element has been checked
	{
		if(score[i]>60.00 && score[i]<70.0) //print test score if greater than 60.0, but less than 70.0
			outfile<<ID[i]<< " "; 
	}
	return;
    }

    void PrintScoreF(ofstream &outfile, int ID[], float score[], int &elementsUsed)
			// Recieves - the output file, array of student IDs, array of test scores, and elements used
			// Task - Prints tests score that are less than 60.0
			// Returns - Nothing
    {
	int i;
	for(i=0; i<elementsUsed; ++i) //continue in the loop until every element has been checked
	{
		if(score[i]<60.0)
			outfile<<ID[i]<< " "; //print test score if it is less than 60.0
	}
	return;
    }

    void FindLowScore(float scores[], int &elementsUsed, int &ls)
			// Recieves - the array of test scores, elements used, and the low score
			// Task - Finds the lowest value location in the array of test scores
			// Returns - Nothing
    {
	int i;
	int minVal = 110; //Initialize a minimum value that is greater than the maximum value, which is 100
	ls = 0;
	for(i=0; i<elementsUsed; i++) //Continue in the loop until each value read in has been checked
	{
		if(minVal > scores[i]) //Check to see if the minimum value is greater than the current array value 
		{
			minVal = scores[i]; //Replace the minimum value with the current array value
			ls = i; //Replace the index location of the minimum with the value assigned to ls 
		}
	}
	return;
    }

    void FindHighScore(float scores[], int &elementsUsed, int &hs)
			// Recieves - The array of student IDs, elements used, and the high score
			// Task - Finds the highest score location in the array of test scores
			// Returns - Nothing
    {
	int i;
	int maxVal = -1; //Initialize a maximum value that less than the minimum value, which is 0
	for(i=0; i<elementsUsed; i++) //Continue in the loop until each value read in has been check
	{
		if(maxVal < scores[i]) //Check to see if the maximum value is less than the current array value
		{
			maxVal = scores[i]; //Replace the maximum value with the current array value
			hs = i; //Replace the index location of the maximum with the value assigned to hs 
		}
	}
	return;
    }

    void FindAverage(float scores[], int &elementsUsed, float &total)
			// Recieves - the array of scores, elements used, and the total
			// Task - Compute the total sum of all the test scores
			// Returns - Nothing
    { 
	int i;
	total = 0;

	for(i=0; i<elementsUsed; ++i) //Check each value read in
	{
		total += scores[i]; //Add the test score in the current array value to total
	}
	return;
    }
