# task1-pdp
import java.util.ArrayList;
import java.util.List;
import java.util.UUID;

// Value Objects layer
class ProductID {
    private final String id;
    public ProductID(String id) { this.id = id; }
    public String getId() { return id; }
}

class ReleaseID {
    private final String id;
    public ReleaseID(String id) { this.id = id; }
    public String getId() { return id; }
}

class SprintID {
    private final String id;
    public SprintID(String id) { this.id = id; }
    public String getId() { return id; }
}

// Entities layer

// Aggregate Root: Backlog
class Backlog {
    private UUID id;
    private String name;
    private List<BacklogItem> items = new ArrayList<>();

    public Backlog(String name) {
        this.id = UUID.randomUUID();
        this.name = name;
    }

    public void addItem(BacklogItem item) { items.add(item); }
    public UUID getId() { return id; }
    public String getName() { return name; }
    public List<BacklogItem> getItems() { return items; }
}

// Entity 
class BacklogItem {
    private UUID id;
    private String summary;
    private List<Task> tasks = new ArrayList<>();
    private ProductID productID;
    private ReleaseID releaseID;
    private SprintID sprintID;

    public BacklogItem(String summary, ProductID productID, ReleaseID releaseID, SprintID sprintID) {
        this.id = UUID.randomUUID();
        this.summary = summary;
        this.productID = productID;
        this.releaseID = releaseID;
        this.sprintID = sprintID;
    }

    public void addTask(Task task) { tasks.add(task); }
    public UUID getId() { return id; }
    public String getSummary() { return summary; }
    public List<Task> getTasks() { return tasks; }
    public ProductID getProductID() { return productID; }
    public ReleaseID getReleaseID() { return releaseID; }
    public SprintID getSprintID() { return sprintID; }
}

// Entity
class Task {
    private UUID id;
    private String description;

    public Task(String description) {
        this.id = UUID.randomUUID();
        this.description = description;
    }

    public UUID getId() { return id; }
    public String getDescription() { return description; }
}

// Application layer

public class ProjectManagementApp {
    public static void main(String[] args) {
        // Initialize entities and value objects to simulate a real-world application scenario.
        Backlog backlog = new Backlog("Project Alpha");
        ProductID productID = new ProductID("P123");
        ReleaseID releaseID = new ReleaseID("R456");
        SprintID sprintID = new SprintID("S789");

        BacklogItem feature1 = new BacklogItem("Implement login feature", productID, releaseID, sprintID);
        feature1.addTask(new Task("Design the login page"));
        feature1.addTask(new Task("Implement authentication logic"));
        
        backlog.addItem(feature1);

        // Simple output
        System.out.println("Backlog: " + backlog.getName());
        for (BacklogItem item : backlog.getItems()) {
            System.out.println("Item: " + item.getSummary());
            for (Task task : item.getTasks()) {
                System.out.println("  Task: " + task.getDescription());
            }
        }
    }
}
