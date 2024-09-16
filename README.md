// RS-Agarwal-Calendar
// Finding day of the week using RS Agarwal's calendar algorithm
import java.util.Scanner;

public class RSAgarwalCalendar {

    public static int findDay(int day, int month, int year) {
        
        //month code
        int[] monthCode = {0, 3, 3, 6, 1, 4, 6, 2, 5, 0, 3, 5}; 
        
        if (isLeapYear(year) && (month == 1 || month == 2)) {
            monthCode[0] = 6; //jan
            monthCode[1] = 2; //feb
        }
        
        int[] cc = {6,4,2,0,6}; //Century code
        int i=0, centuryCode=0;
        for (int yc=16; yc<=20; yc++){
            if(year/100 == yc){
                centuryCode= cc[i];
            }
            i++;
        }

        int lastTwoDigitsOfYear = year % 100; //year

        int leapYearAdjustment = lastTwoDigitsOfYear / 4; //year code        
    
        int total = (day + monthCode[month - 1] + lastTwoDigitsOfYear + leapYearAdjustment + centuryCode) % 7;

        if (isLeapYear(year)){
            return total-1;
        }
        else{
            return total;
        }
    }
        

    // leap year
    public static boolean isLeapYear(int year) {
        if ((year/4 == 0 && year/100 != 0) || year % 400 == 0) {
            return true;
        }
        return false;
    }


    // days in month
    public static int daysInMonth(int month, int year) {
        switch (month) {
            case 1:  // January
            case 3:  // March
            case 5:  // May
            case 7:  // July
            case 8:  // August
            case 10: // October
            case 12: // December
                return 31;
            case 4:  // April
            case 6:  // June
            case 9:  // September
            case 11: // November
                return 30;
            case 2:  // February
                return isLeapYear(year) ? 29 : 28;
            default:
                return 0; // Invalid month
        }
    }

    
    // display
    public static void display(int month, int year) {

        System.out.println(" Sun Mon Tue Wed Thu Fri Sat");

        int firstDay = findDay(1, month, year);

        int daysInMonth = daysInMonth(month, year);

        for (int i = 0; i < firstDay; i++) {
            System.out.print("    ");
        }

        for (int day = 1; day <= daysInMonth; day++) {
            System.out.printf("%4d", day);
            if ((day + firstDay) % 7 == 0) {
                System.out.println();
            }
        }
        System.out.println();
    }


    public static void main(String[] args) {
      
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter date: ");
        int day = sc.nextInt();

        System.out.print("Enter month (1-12): ");
        int month = sc.nextInt();

        System.out.print("Enter year (1600-2099): ");
        int year = sc.nextInt();

        String[] dayWeek = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};

        String dayOfWeek = dayWeek[findDay(day, month, year)];

        System.out.println("The day of the week is: " + dayOfWeek);

        System.out.println("\nCalendar for " + month + "/" + year + ":");
        display(month, year);

    }
}

