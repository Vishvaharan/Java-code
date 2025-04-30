import java.util.Scanner;

class Movie {
    String movieName;
    int availableSeats;
    double adultTicketPrice;
    double childTicketPrice;
    double seniorTicketPrice;

    // Constructor to initialize movie details
    public Movie(String movieName, int availableSeats, double adultTicketPrice, double childTicketPrice, double seniorTicketPrice) {
        this.movieName = movieName;
        this.availableSeats = availableSeats;
        this.adultTicketPrice = adultTicketPrice;
        this.childTicketPrice = childTicketPrice;
        this.seniorTicketPrice = seniorTicketPrice;
    }

    // Method to calculate total price based on ticket type
    public double calculateTotalPrice(int numTickets, String ticketType) {
        double price = 0.0;
        if (ticketType.equalsIgnoreCase("adult")) {
            price = adultTicketPrice * numTickets;
        } else if (ticketType.equalsIgnoreCase("child")) {
            price = childTicketPrice * numTickets;
        } else if (ticketType.equalsIgnoreCase("senior")) {
            price = seniorTicketPrice * numTickets;
        }
        return price;
    }
    
    // Method to update available seats after booking
    public void updateAvailableSeats(int numTickets) {
        this.availableSeats -= numTickets;
    }

    // Method to check if enough seats are available
    public boolean checkAvailableSeats(int numTickets) {
        return numTickets <= availableSeats;
    }
}

public class MovieAndShowBookingSystem {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Create movie objects with show timings and pricing
        Movie movie1 = new Movie("Good Bad Ugly", 50, 300.00, 150.00, 200.00);
        Movie movie2 = new Movie("Dragon", 30, 400.00, 200.00, 250.00);
        Movie movie3 = new Movie("Kanguva", 20, 350.00, 175.00, 220.00);


        boolean continueBooking = true;

        while (continueBooking) {
            // Movie selection
            System.out.println("Welcome to the Movie Booking System!");
            System.out.println("Available Movies:");
            System.out.println("1. " + movie1.movieName);
            System.out.println("2. " + movie2.movieName);
            System.out.println("3. " + movie3.movieName);
            System.out.print("Enter movie number (1, 2, or 3): ");
            
            int movieChoice = sc.nextInt();
            Movie selectedMovie = null;

            if (movieChoice == 1) {
                selectedMovie = movie1;
            } else if (movieChoice == 2) {
                selectedMovie = movie2;
            } else if (movieChoice == 3) {
                selectedMovie = movie3;
            } else {
                System.out.println("Invalid choice. Exiting the system.");
                return;
            }

            // Show timings selection
            System.out.println("\nAvailable Show Timings for " + selectedMovie.movieName + ":");
            System.out.println("1. 2:00 PM");
            System.out.println("2. 5:00 PM");
            System.out.println("3. 8:00 PM");
            System.out.print("Select the show timing (1, 2, or 3): ");
            int showChoice = sc.nextInt();

            // Show selected details
            System.out.println("\nYou selected: " + selectedMovie.movieName);
            System.out.println("Show Time: " + (showChoice == 1 ? "2:00 PM" : showChoice == 2 ? "5:00 PM" : "8:00 PM"));
            System.out.println("Available Seats: " + selectedMovie.availableSeats);

            // Ticket Type selection
            System.out.println("\nSelect the ticket type:");
            System.out.println("1. Adult ($" + selectedMovie.adultTicketPrice + ")");
            System.out.println("2. Child ($" + selectedMovie.childTicketPrice + ")");
            System.out.println("3. Senior ($" + selectedMovie.seniorTicketPrice + ")");
            System.out.print("Enter ticket type (1, 2, or 3): ");
            int ticketTypeChoice = sc.nextInt();
            String ticketType = "";

            if (ticketTypeChoice == 1) {
                ticketType = "adult";
            } else if (ticketTypeChoice == 2) {
                ticketType = "child";
            } else if (ticketTypeChoice == 3) {
                ticketType = "senior";
            } else {
                System.out.println("Invalid choice. Exiting the system.");
                return;
            }

            // Ask for number of tickets
            System.out.print("\nEnter number of tickets to book: ");
            int numTickets = sc.nextInt();

            // Check seat availability
            if (selectedMovie.checkAvailableSeats(numTickets)) {
                // Calculate total price
                double totalPrice = selectedMovie.calculateTotalPrice(numTickets, ticketType);
                System.out.println("Total price for " + numTickets + " " + ticketType + " tickets: $" + totalPrice);

                // Ask for booking confirmation
                System.out.print("Do you want to confirm the booking? (yes/no): ");
                String confirm = sc.next();

                if (confirm.equalsIgnoreCase("yes")) {
                    // Update available seats after booking
                    selectedMovie.updateAvailableSeats(numTickets);
                    System.out.println("Booking confirmed!");
                    System.out.println("Remaining seats: " + selectedMovie.availableSeats);
                } else {
                    System.out.println("Booking canceled.");
                }
            } else {
                System.out.println("Not enough seats available. Only " + selectedMovie.availableSeats + " seats left.");
            }

            // Ask if the user wants to book another ticket
            System.out.print("\nDo you want to book another ticket? (yes/no): ");
            String anotherBooking = sc.next();

            if (anotherBooking.equalsIgnoreCase("no")) {
                continueBooking = false;
            }
        }

        System.out.println("Thank you for using the Movie Booking System. Goodbye!");
        sc.close();
    }
}
