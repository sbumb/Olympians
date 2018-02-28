# Olympians
Java Coursework
Program to take in Olympian information, store it to an ArrayList, then send that information to a text file in table format.

    import java.util.ArrayList;
    import java.util.Scanner;
    import java.io.File;
    import java.io.FileNotFoundException;
    import java.io.PrintWriter;

    //Pre-processor--------------------------------------------------------------------------------------------------------------------

    public class Olympian {//openClass
      private String name;
      private String sport;
      private int numMedals;
      private String event;

      static Scanner sc = new Scanner(System.in);


      public Olympian(String name, String sport, String event,int numMedals){//openConstructor
        this.name = name;
        this.sport = sport;
        this.numMedals = numMedals;
        this.event = event;


      }//closeConstructor------------------------------------------------------------------------------------------------------------

      public static int computeMedals(ArrayList<Olympian> olympians){//opencomputeMedals

        int totalMedals = 0;
        
        for(Olympian o : olympians){//openFor
          totalMedals += o.numMedals;
        }//closeFor

        return totalMedals;

      }//closecomputeMedals----------------------------------------------------------------------------------------------------------

      public String toString(){//opentoString
        return String.format("%-22s%-22s%-22s%-22s",name,sport,event,numMedals);

      }//closetoString----------------------------------------------------------------------------------------------------------------

      public static void main  (String args[]) throws FileNotFoundException{
        PrintWriter pw = new PrintWriter(new File("results.txt"));
        pw.println("P3: Olympians \nSteven Bumbera\n");
        pw.println("Please enter the name, sport, event, and medals earned by your Olympian! ");
        pw.println("Please press lowercase q on Name, Sport, or Event\n "
            + "to end the program. Or press 11 on medals! \n\n" + System.getProperty("line.separator"));

        ArrayList<Olympian> olympians = new ArrayList<>();
        String name = "";
        String sport = "";
        String event = "";
        int numMedals = 0;


        for(;;){
          System.out.println("Enter Olympian's NAME: ");
          name = sc.nextLine();
          if(name.equals("q"))break;

          System.out.println("Enter Olympian's SPORT: ");
          sport = sc.nextLine();
          if(sport.equals("q"))break;

          System.out.println("Enter Olympian's EVENT: ");
          event = sc.nextLine();
          if(event.equals("q"))break;

          System.out.println("Enter Olympian's medals: ");
          numMedals = Integer.parseInt(sc.nextLine());
          if(numMedals < 0 || numMedals > 10)break;

          olympians.add(new Olympian(name,sport,event,numMedals) );

        }//closeFor----------------------------------------------------------------------------------------------------------------

        pw.printf("%-22s%-22s%-22s%-22s ","NAME","SPORT","EVENT","MEDALS" );
        for(Olympian o : olympians) {

          pw.println(System.getProperty("line.separator") + o);
        }
        pw.printf("\t\t\t\t\t\t   TOTAL MEDALS = " + computeMedals(olympians) + System.getProperty("line.separator"));
        pw.println("Thank you for using my program!\n"
            + "I hope you'll come back when I'm better at this!");
        pw.close();
        }//endMain
    }//endClass
