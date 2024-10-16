# BootCamp-Day--2
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

class LiftManagement {
    private Queue<Integer> floorQueue;
    private int currentFloor;

    public LiftManagement() {
        floorQueue = new LinkedList<>();
        currentFloor = 0; // Assuming the lift starts at ground floor (0)
    }

    // Add a floor request to the queue
    public void requestFloor(int floor) {
        if (floor != currentFloor) {
            System.out.println("Floor " + floor + " requested.");
            floorQueue.add(floor);
        } else {
            System.out.println("Lift is already on floor " + floor);
        }
    }

    // Process the next floor request in the queue
    public void moveLift() {
        if (!floorQueue.isEmpty()) {
            int nextFloor = floorQueue.poll(); // Remove the next floor from the queue
            System.out.println("Moving lift from floor " + currentFloor + " to floor " + nextFloor);
            currentFloor = nextFloor;
        } else {
            System.out.println("No more floor requests.");
        }
    }

    // Get the current floor of the lift
    public int getCurrentFloor() {
        return currentFloor;
    }

    public boolean hasPendingRequests() {
        return !floorQueue.isEmpty();
    }
}

public class LiftManagementSystem {
    public static void main(String[] args) {
        LiftManagement lift = new LiftManagement();
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while (running) {
            System.out.println("\nCurrent Floor: " + lift.getCurrentFloor());
            System.out.println("1. Request a floor");
            System.out.println("2. Move lift");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();

            switch (option) {
                case 1:
                    System.out.print("Enter floor number to request: ");
                    int floor = scanner.nextInt();
                    lift.requestFloor(floor);
                    break;

                case 2:
                    lift.moveLift();
                    break;

                case 3:
                    running = false;
                    System.out.println("Exiting lift management system.");
                    break;

                default:
                    System.out.println("Invalid option. Please try again.");
            }

            // If there are pending requests, automatically process them
            while (lift.hasPendingRequests()) {
                lift.moveLift();
            }
        }

        scanner.close();
    }
}
