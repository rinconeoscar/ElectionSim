# ElectionSim
Able to simulate elections given statistics
//ElectionSimulator
//Creating a simple type of election simulator relative to what professional analyst use to predict multiple outcomes of said
//election which values given to us. 
import java.util.*;

//Election Simulator which runs mutliple simulations of said election in a given amount of districts.
public class ElectionSimulator {
        public static final int NUM_SIMS = 5;
        public static final int NUM_DISTS = 10;
        public static final double POLL_ERR = .07;
        public static final double POLL_AVG = .52;
        //* Main method prints sim statements with given values
        public static void main(String[] args){ 
                Random randy = new Random();
                double avgPerc = 0.0;

                System.out.println("Welcome to the Election Simulator!");
                System.out.println("Running " + NUM_SIMS + " simulations of " + NUM_DISTS + " districts." );
                System.out.println("Our candidate is polling at " + POLL_AVG * 100 + "% with a " + POLL_ERR * 100 + "% margin of error.");
                System.out.println();
                //* Main loop runs simulation NUM_SIM times
                for(int i = 1; i <= NUM_SIMS; i++){
                        System.out.println("Running simulation #" + i + ":");
                        int votePer1 = 0;
                        int votePer2 = 0;
                        int votes = 0;
                        double per1Perc = 0.0;
                        double per2Perc = 0.0;
                        //* Nested loop to find and combine random values
                        for (int kk = 1; kk <= NUM_DISTS; kk++){
                                int tomo = randy.nextInt(1000) + 1;
                                double randVotePerc = randy.nextGaussian() * 0.5 * POLL_ERR;
                                double randVotePerc0 = randVotePerc + POLL_AVG;
                                double distPerCount = tomo * randVotePerc0;

                                votePer1 = votePer1 + (int)distPerCount;
                                votes = votes + tomo;
                }
                                per1Perc =  (double)votePer1 / votes;
                                votePer2 = (votes - votePer1); 
                                per2Perc = 1.0*votePer2/votes;   
                                //check if win cuz over 50%
                                boolean win =  votePer1 > votePer2;
                                double per1SimAvg= per1Perc/NUM_DISTS;
                                double per2SimAvg = per2Perc/NUM_DISTS;
                                avgPerc = avgPerc + per1Perc;
                                //print out text with the values needed, also finding percentage
                                System.out.println("  Win? " + win);
                                System.out.print("  Results: " + votePer1 + " (" + (per1Perc*100.0) + "%)");
                                System.out.println(" - " + votePer2 + " (" + (per2Perc*100.0) + "%)");
                                System.out.print("  Visualization: ");
                                //loop that prints out +'s for every 100 votes
                                for(int l = 100; l < votePer1; l += 100) {
                                        System.out.print("+");
                }
                                        System.out.println();
                                        System.out.print("                 ");
                                                //loop that prints out -'s for every 100 votes opponent gets
                                        for(int q = 100; q < votePer2; q += 100){
                                                System.out.print("-");
                }
               
                                                System.out.println();
                }
                                                //prints out avg percentage
                                                System.out.println("Average vote percentage: " + (avgPerc/NUM_SIMS*100.0) + "%" );
        }
        }
