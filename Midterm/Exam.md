```java

public class Drug{

    private String itemName;
    private String companyName;

    public Drug(){
        itemName = "None";
        companyName = "None";

    }

    public Drug(String itemName, String companyName){
        this.itemName = itemName;
        this.companyName = companyName;

    }

    public void updateItemName(String newItemName){
        itemName = newItemName;
        System.out.println("Item Name Updated.");
    }

    public void updateCompanyName(String newCompanyName){
        companyName = newCompanyName;
        System.out.println("Company Name Updated.");
    }

    public void displayItems(){
        System.out.println("Item Name: " + itemName);
        System.out.println("Company Name: " + companyName);

    }

}

public class Painkillers extends Drug{
    
    private String expiryDate;
    private String ageGroup;
    
    public Painkillers(String itemName, String companyName, String expiryDate, String ageGroup){
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;

    }
    
    public void updateExpiryDate(String newExpiryDate){
        expiryDate = newExpiryDate;
        System.out.println("Expiry Date Updated.");
    }
    
    public void updateAgeGroup(String newAgeGroup){
        ageGroup = newAgeGroup;
        System.out.println("Age Group Updated.");
    }
    
    @Override
    public void displayItems(){
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
    }


}
public class Bandages extends Drug{
    
    private String expiryDate;
    private String ageGroup;
    private String waterProof;
    
    public Bandages(String itemName, String companyName, String expiryDate, String ageGroup, String waterProof){
        super(itemName, companyName);
        this.expiryDate = expiryDate;
        this.ageGroup = ageGroup;
        this.waterProof = waterProof;
    }
    
    public void updateExpiryDate(String newExpiryDate){
        expiryDate = newExpiryDate;
        System.out.println("Expiry Date Updated.");
    }
    
    public void updateAgeGroup(String newAgeGroup){
        ageGroup = newAgeGroup;
        System.out.println("Age Group Updated.");
    }
    
    public void updateWaterProof(String newWaterProof){
        waterProof = newWaterProof;
        System.out.println("Water Proofing Updated.");
    }
    
    @Override
    public void displayItems(){
        System.out.println("Expiry Date: " + expiryDate);
        System.out.println("Age Group: " + ageGroup);
        System.out.println("Water Proof(Y/N): " + waterProof);
    }


}

public class Equipment extends Drug{
    int itemWeight;
    
    public Equipment(String itemName, String companyName, int itemWeight){
        super(itemName, companyName);
        this.itemWeight = itemWeight;
    }
    
    public void updateItemWeight(int newItemWeight){
        itemWeight = newItemWeight;
        System.out.println("Item Weight Updated.");
    }
    
    @Override
    public void displayItems(){
        System.out.println("Item Weight(lbs): " + itemWeight);
    }


}

import java.util.Scanner;
public class DrugDemo{
    public static void main(String[] args){
    
        Scanner keyboard = new Scanner(System.in);
        try{
        Painkillers pain = new Painkillers("OxyContin", "Purdue", "01/01/2027", "18+");
        Bandages bandage = new Bandages("Band-Aid", "Johnson & Johnson", "01/01/2031", "Any", "Y");
        Equipment equipment = new Equipment("Ventilator", "Hamilton Medical", 40);
        
        pain.displayItems();
        bandage.displayItems();
        equipment.displayItems();
        
        System.out.println("Enter new drug name: ");
        String newItemName = keyboard.nextLine();
        System.out.println("Enter new manufacturer: ");
        String newCompanyName = keyboard.nextLine();
        System.out.println("Enter new expiry date: ");
        String newExpiryDate = keyboard.nextLine();
        System.out.println("Enter new age group: ");
        String newAgeGroup = keyboard.nextLine();
        
        pain.updateItemName(newItemName);
        pain.updateCompanyName(newCompanyName);
        pain.updateExpiryDate(newExpiryDate);
        pain.updateAgeGroup(newAgeGroup);
        pain.displayItems();
        
        System.out.println("Enter new bandage name: ");
        String newBandageName = keyboard.nextLine();
        System.out.println("Enter new manufacturer: ");
        String newBandageMfg = keyboard.nextLine();
        System.out.println("Enter new expiry date: ");
        String newBandageExpiry = keyboard.nextLine();
        System.out.println("Enter new age group: ");
        String newBandageAge = keyboard.nextLine();
        System.out.println("Waterproof(Y/N): ");
        String newBandageWaterProof = keyboard.nextLine();
        
        bandage.updateItemName(newBandageName);
        bandage.updateCompanyName(newBandageMfg);
        bandage.updateExpiryDate(newBandageExpiry);
        bandage.updateAgeGroup(newBandageAge);
        bandage.updateWaterProof(newBandageWaterProof);
        bandage.displayItems();
        
        System.out.println("Enter new equipment name: ");
        String newEquip = keyboard.nextLine();
        System.out.println("Enter new manufacturer: ");
        String newEquipMfg = keyboard.nextLine();
        System.out.println("Enter new Item Weight(lbs): ");
        int newItemWeight = keyboard.nextInt();
        
        equipment.updateItemName(newEquip);
        equipment.updateCompanyName(newEquipMfg);
        equipment.updateItemWeight(newItemWeight);
        equipment.displayItems();
  }     catch(InputMismatchException e){
        System.out.println("Invalid input. Please enter a valid input.");
    }catch(Exception e){
        System.out.println("An unexpected error occurred: " + e.getMessage());
    
    }
    
    }
}
```
### my attempt at custom exception class. ran out of time
```java
class InvalidInputException extends Exception {
    public InvalidInputException(String message) {
        super(message);
    }
}
```




