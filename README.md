using System;



class Student

{

    public string IndexNumber;

    public string Name;

    public double GPA;

    public int AdmissionYear;

    public string NIC;



    

    public void ShowInfo()

    {

        Console.WriteLine("Index: {IndexNumber}, Name: {Name}, GPA: {GPA}, Year: {AdmissionYear}, NIC: {NIC}");

    }

}



class StudentNode

{

    public Student student;

    public StudentNode next;

}



class StudentLinkedList

{

    private StudentNode head = null;



    

    public void AddStudent(Student newStudent)

    {

        StudentNode newNode = new StudentNode();

        newNode.student = newStudent;



        

        if (head == null || string.Compare(newStudent.IndexNumber, head.student.IndexNumber) < 0)

        {

            if (head != null && head.student.IndexNumber == newStudent.IndexNumber)

            {

                Console.WriteLine("A student with this index number already exists.");

                return;

            }



            newNode.next = head;

            head = newNode;

            Console.WriteLine("Student added successfully.");

            return;

        }



        

        StudentNode current = head;

        while (current.next != null && string.Compare(current.next.student.IndexNumber, newStudent.IndexNumber) < 0)

        {

            current = current.next;

        }



        if (current.next != null && current.next.student.IndexNumber == newStudent.IndexNumber)

        {

            Console.WriteLine("A student with this index number already exists.");

            return;

        }



        newNode.next = current.next;

        current.next = newNode;

        Console.WriteLine("Student added successfully.");

    }



    

    public void FindStudent(string indexNumber)

    {

        StudentNode current = head;



        while (current != null)

        {

            if (current.student.IndexNumber == indexNumber)

            {

                Console.WriteLine("Student found:");

                current.student.ShowInfo();

                return;

            }

            current = current.next;

        }



        Console.WriteLine("Student not found.");

    }



    

    public void RemoveStudent(string indexNumber)

    {

        StudentNode current = head;

        StudentNode previous = null;



        while (current != null)

        {

            if (current.student.IndexNumber == indexNumber)

            {

                if (previous == null)

                {

                    head = current.next;  

                }

                else

                {

                    previous.next = current.next;  

                }



                Console.WriteLine("Student removed.");

                return;

            }



            previous = current;

            current = current.next;

        }



        Console.WriteLine("Student not found.");

    }



    

    public void ShowAllStudents()

    {

        if (head == null)

        {

            Console.WriteLine("No students in the list.");

            return;

        }



        Console.WriteLine("All Students:");

        StudentNode current = head;



        while (current != null)

        {

            current.student.ShowInfo();

            current = current.next;

        }

    }

}



class Program

{

    static void Main()

    {

        StudentLinkedList studentList = new StudentLinkedList();



        while (true)

        {

            Console.WriteLine("Student Management Menu ");

            Console.WriteLine("1 Add New Student");

            Console.WriteLine("2 Search Student");

            Console.WriteLine("3 Delete Student");

            Console.WriteLine("4 Show All Students");

            Console.WriteLine("5 Exit");

            Console.Write(" Enter your choice : ");

            string choice = Console.ReadLine();



            if (choice == "1")

            {

                Student student = new Student();



                Console.Write("Enter Index Number : ");

                student.IndexNumber = Console.ReadLine();



                Console.Write("Enter Name: ");

                student.Name = Console.ReadLine();



                Console.Write("Enter GPA: ");

                student.GPA = Convert.ToDouble(Console.ReadLine());



                Console.Write("Enter Admission Year: ");

                student.AdmissionYear = Convert.ToInt32(Console.ReadLine());



                Console.Write("Enter NIC: ");

                student.NIC = Console.ReadLine();



                studentList.AddStudent(student);

            }

            else if (choice == "2")

            {

                Console.Write("Enter Index Number to search: ");

                string index = Console.ReadLine();

                studentList.FindStudent(index);

            }

            else if (choice == "3")

            {

                Console.Write("Enter Index Number to delete: ");

                string index = Console.ReadLine();

                studentList.RemoveStudent(index);

            }

            else if (choice == "4")

            {

                studentList.ShowAllStudents();

            }

            else if (choice == "5")

            {

                Console.WriteLine("Exiting program.");

                break;

            }

            else

            {

                Console.WriteLine("Invalid choice. Please enter a number between 1 and 5.");

            }

        }

    }

}


