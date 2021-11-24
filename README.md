# BSI

autorzy patcha:
Mikołaj Jakubowski
Kamil Głowienke

patch jest do repo: https://github.com/AdSten/Space-Challenge

Błąd OBJ01 - wrażliwe zmienne powinny być prywatne
Błąd OBJ07 - nie powinno się móc kopiować wrażliwych klas


-public class Rocket implements SpaceShip{
-    int cost;
-    int weight;
-    int maxWeight;
+public final class Rocket implements SpaceShip{
+    private int cost;
+    private int weight;
+    private int maxWeight;

     public boolean launch() {
         return true;
        
public class Rocket implements SpaceShip{
     public void carry(Item item) {
         weight += item.weight;
     }
+
+    public int getCost() {
+        return cost;
+    }
+
+    public int getWeight() {
+        return weight;
+    }
+
+    public int getMaxWeight() {
+        return maxWeight;
+    }
+
+
+    public void setCost(int cost) {
+        this.cost = cost;
+    }
+
+    public void setWeight(int weight) {
+        this.weight = weight;
+    }
+
+    public void setMaxWeight(int maxWeight) {
+        this.maxWeight = maxWeight;
+    }
 }
 
 
Błąd ERR00 - nie ignorować wyjątków typu checked

 public class Simulation {
 
-   ArrayList<Item> loadItems(String fileName) throws Exception{
+   ArrayList<Item> loadItems(String fileName){
         File file = new File(fileName);
-        Scanner scan = new Scanner(file);
-        ArrayList<Item>items = new ArrayList<>();
+       Scanner scan = null;
+       try {
+           scan = new Scanner(file);
+       } catch (FileNotFoundException e) {
+           System.out.println("Please use different file name");
+            Scanner scanner = new Scanner(System.in);
+            String filename = scanner.nextLine();
+            loadItems(fileName);
+       }
+       ArrayList<Item>items = new ArrayList<>();
 
         while(scan.hasNextLine()){
             String line = scan.nextLine();
