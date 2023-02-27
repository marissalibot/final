using System;

namespace EmployeeTimeKeeping 
{
    class Program
    {
        static void Main(string[] args)
        {
        TimeSpan workStart = new TimeSpan(7, 0, 0);
        TimeSpan workEnd = new TimeSpan(17, 0, 0);
        TimeSpan gracePeriod = new TimeSpan(0, 15, 0);
        
        Console.Write("Enter employee ID: ");
        string employeeId = Console.ReadLine();
        
    if (employeeId != "12345")
    {
    Console.WriteLine("Error: Invalid employee ID");
    return;
    }
    Console.Write("Enter Full name: ");
    string fullName = Console.ReadLine();
    Console.Write("Enter Department: ");
    string department = Console.ReadLine();
    
    Console.Write("Enter time-in (HH:mm:ss): ");
    TimeSpan timeIn = TimeSpan.Parse(Console.ReadLine());
    Console.Write("Enter time-out (HH:mm:ss): ");
    TimeSpan timeOut = TimeSpan.Parse(Console.ReadLine());
    TimeSpan totalHours = timeOut - timeIn;
    
    TimeSpan regularHours = TimeSpan.Zero;
    if (timeIn < workStart)
    {
     regularHours += workStart - timeIn;
    }
    if (timeOut > workEnd)
    {
     regularHours += workEnd - (timeIn > workStart ? timeIn : workStart);
    }
    else
    {
     regularHours += timeOut - (timeIn > workStart ? timeIn : workStart);
    }
    
    TimeSpan lateTime = TimeSpan.Zero;
    if (timeIn > workStart + gracePeriod)
    {
     lateTime = timeIn - workStart - gracePeriod;
    }
    TimeSpan undertime = TimeSpan.Zero;
    if (totalHours < regularHours)
    {
     undertime = regularHours - totalHours;
    }
    TimeSpan overtime = TimeSpan.Zero;
    if (totalHours > regularHours)
    {
     overtime = totalHours - regularHours;
    }
    Console.WriteLine($"Total hours worked: {totalHours}");
    Console.WriteLine($"Regular hours worked: {regularHours}");
    Console.WriteLine($"Late time: {lateTime}");
    Console.WriteLine($"Undertime: {undertime}");
    Console.WriteLine($"Overtime: {overtime}");
    
      }
   }
}
