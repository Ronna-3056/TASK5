using System;
using System.Linq;

namespace StudentReportCard
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter Total Students : ");
            int totalStudents = int.Parse(Console.ReadLine());

            // Multi-dimensional array: [Row, Column]
            // Columns: 0=Name, 1=English, 2=Math, 3=Computer, 4=Total Marks
            string[,] studentData = new string[totalStudents, 5];

            // 1. Data Entry Loop
            for (int i = 0; i < totalStudents; i++)
            {
                Console.Write("Enter Student Name : ");
                studentData[i, 0] = Console.ReadLine();

                Console.Write("Enter English Marks (Out Of 100) : ");
                int eng = int.Parse(Console.ReadLine());
                studentData[i, 1] = eng.ToString();

                Console.Write("Enter Math Marks (Out Of 100) : ");
                int math = int.Parse(Console.ReadLine());
                studentData[i, 2] = math.ToString();

                Console.Write("Enter Computer Marks (Out Of 100) : ");
                int comp = int.Parse(Console.ReadLine());
                studentData[i, 3] = comp.ToString();

                // Calculate Total
                int total = eng + math + comp;
                studentData[i, 4] = total.ToString();

                Console.WriteLine("*********************************************");
            }

            // 2. Sorting Logic (Descending Order based on Total Marks)
            // We use a simple Bubble Sort to rearrange the rows in the 2D array
            
            for (int i = 0; i < totalStudents - 1; i++)
            {
                for (int j = 0; j < totalStudents - i - 1; j++)
                {
                    if (int.Parse(studentData[j, 4]) < int.Parse(studentData[j + 1, 4]))
                    {
                        // Swap rows
                        for (int k = 0; k < 5; k++)
                        {
                            string temp = studentData[j, k];
                            studentData[j, k] = studentData[j + 1, k];
                            studentData[j + 1, k] = temp;
                        }
                    }
                }
            }

            // 3. Output Report Card
            Console.WriteLine("****************Report Card*******************");
            for (int i = 0; i < totalStudents; i++)
            {
                Console.WriteLine("****************************************");
                Console.WriteLine($"Student Name: {studentData[i, 0]}, Position: {i + 1}, Total: {studentData[i, 4]}/300");
            }
            Console.WriteLine("****************************************");
        }
    }
}
