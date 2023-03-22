# Covid-calculate-program
a simple program that has many OOP concepts to calculate number of Diseased countries and treatment cost etc.  
public class FinalExam {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // Q.1 
        Country country[] = new Country[2]; // Array of type Country 
        country[0] = new Country("Saudi Arabia", new Capital("Riyadh"), "SAR", 0.27); // First Object 
        country[1] = new Country("Jordan", new Capital("Amman"), "JD", 1.41); // Second Object 
        
        for ( Country i : country ){ // enhanced for loop to print all the data of the objects 
            System.out.println(i.toString());
        }
        //Q.2 
        System.out.println("--------------------"); // To make things clear a bit 
        
        Cholera cholera[] = new Cholera[4]; // Array Of Objects of type Cholera
        
        cholera[0] = new Cholera("Cholera", "Italy", 45, 120); // First Object 
        cholera[1] = new Cholera("Cholera", "USA", 52, 120);   // Second Object 
        cholera[2] = new Cholera("Cholera", "Spain", 37, 120); // Third Object
        cholera[3] = new Cholera("Cholera", "China", 6, 120);  // Fourth Object 
        
        int total = 0, a, b, c, d; // Variables 
        for ( Cholera i : cholera ){ // enhanced for loop to print the total people that has the diseas 
            total += i.getNumberOfInfectedPersons();
        }
        System.out.println("Total number of infected persons in all countries = "+total);
        
        a = cholera[0].getNumberOfInfectedPersons(); // a = the number of infected  
        b = cholera[1].getNumberOfInfectedPersons(); // b = the number of infected  
        c = cholera[2].getNumberOfInfectedPersons(); // c = the number of infected  
        d = cholera[3].getNumberOfInfectedPersons(); // d = the number of infected  
        
        System.out.print("The country that has the highest number of infected is "); // print 
        if ( a > b && a > c && a > d ) // comparison 
            System.out.println(cholera[0].getInfectedCountry());
        if ( b > a && b > c && b > d ) // comparison 
            System.out.println(cholera[1].getInfectedCountry());
        if ( c > a && c > b && c > d ) // comparison 
            System.out.println(cholera[2].getInfectedCountry());
        if ( d > a && d > b && d > c ) // comparison 
            System.out.println(cholera[3].getInfectedCountry());
        
        double treatmentCost = 0; // Variable 
        for ( Cholera x : cholera ){ // enhanced for loop to calculate the total treatment cost of all countries 
            treatmentCost += x.treatmentCost();
        }
        System.out.println("Total cost of all countries: "+ treatmentCost+" US$"); 
        
    }
    
}

class Capital{ // class Capital (Concret)
    private String capiatName; // instance variable 

    public Capital(String capiatName) { // Constructer 
        this.capiatName = capiatName;
    }

    public String getCapiatName() { // getter
        return capiatName;
    }

    public void setCapiatName(String capiatName) { // setter 
        this.capiatName = capiatName;
    }
    
}
class Country{ // class Country 
    private String countryName; // instace variable 
    private Capital capital; // compsition , instance variable  
    private String currencyName; // instace variable  
    private double currencyValue; // instace variable  
    // Constructer 
    public Country(String countryName, Capital capital, String currencyName, double currencyValue) {
        this.countryName = countryName;
        this.capital = capital;
        this.currencyName = currencyName;
        this.currencyValue = currencyValue;
    }

    public String getCurrencyName() { // getter 
        return currencyName;
    }
    
    public double convertToUSDollar(double amount){ // Converting SAR & JD to USA dollar 
        return amount*currencyValue; 
    }

    @Override
    public String toString() { // toString to print all data of the class 
       return "Countery: "+ countryName+", "+"Capital: "+ capital.getCapiatName()+", "
               + "Currency: "+ currencyName+", "+"Value: "+ currencyValue+", "
               + 1000+" "+currencyName+" ="+convertToUSDollar(1000)+" USD";
    }
}

interface Treatable{ // interface Treatable
    public abstract double treatmentCost(); // Abstract method named treatment Cost
}
abstract class Diseas{ // abstract class named Diseas
    private String name; // instance variable 
    private String infectedCountry;  // instance variable  
    private int numberOfInfectedPersons; // instance variable  
    private double medicineCostPerPerson; // instance variable  
    // Constructer 
    public Diseas(String name, String infectedCountry, int numberOfInfectedPersons, double medicineCostPerPerson) {
        this.name = name;
        this.infectedCountry = infectedCountry;
        this.numberOfInfectedPersons = numberOfInfectedPersons;
        this.medicineCostPerPerson = medicineCostPerPerson;
    }

    public String getName() { // getter 
        return name;
    }

    public String getInfectedCountry() { // getter 
        return infectedCountry;
    }

    public int getNumberOfInfectedPersons() { // getter 
        return numberOfInfectedPersons;
    }

    public double getMedicineCostPerPerson() { // getter 
        return medicineCostPerPerson;
    }
    
    public abstract double treatmentCost(); // abstract method named treatmentCost
}
// class cholera extends the Diseas class and implement Treatable interface 
class Cholera extends Diseas implements Treatable{ 
    // constructer 
    public Cholera(String name, String infectedCountry, int numberOfInfectedPersons, double medicineCostPerPerson) {
        super(name, infectedCountry, numberOfInfectedPersons, medicineCostPerPerson);
    }
    
    @Override                       // Override method named treatmentCost wich return the total 
    public double treatmentCost(){ // cost of inefcted Persones 
        return getMedicineCostPerPerson()*getNumberOfInfectedPersons();
    }
}
