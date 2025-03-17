## Thought process for this project: 
## See Derived Classes project. Functionally, very similar project requirements.

```java
public class Book {
    private String title;
    private String author;
    private String publisher;
    private String publicationDate;

    public void setTitle(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getAuthor() {
        return author;
    }

    public void setPublisher(String publisher) {
        this.publisher = publisher;
    }

    public String getPublisher() {
        return publisher;
    }

    public void setPublicationDate(String publicationDate) {
        this.publicationDate = publicationDate;
    }

    public String getPublicationDate() {
        return publicationDate;
    }

    public void printInfo() {
        System.out.println("Book Information:");
        System.out.println(" Book Title: " + getTitle());
        System.out.println(" Author: " + getAuthor());
        System.out.println(" Publisher: " + getPublisher());
        System.out.println(" Publication Date: " + getPublicationDate());
    }
}

public class Encyclopedia extends Book {
    private String edition;
    private int numPages;

    public void setEdition(String edition) {
        this.edition = edition;
    }

    public String getEdition() {
        return edition;
    }

    public void setNumPages(int numPages) {
        this.numPages = numPages;
    }

    public int getNumPages() {
        return numPages;
    }

    @Override
    public void printInfo() {
        super.printInfo(); // Call the base class printInfo method
        System.out.println(" Edition: " + edition);
        System.out.println(" Number of Pages: " + numPages);
    }
}

import java.util.Scanner;

public class BookInfo {
    public static void main(String[] args) {
        Scanner keyboard = new Scanner(System.in);

        Book myBook = new Book();
        Encyclopedia myEncyclopedia = new Encyclopedia();

        String title, author, publisher, publicationDate;
        String eTitle, eAuthor, ePublisher, ePublicationDate, edition;
        int numPages;

        title = keyboard.nextLine();
        author = keyboard.nextLine();
        publisher = keyboard.nextLine();
        publicationDate = keyboard.nextLine();

        eTitle = keyboard.nextLine();
        eAuthor = keyboard.nextLine();
        ePublisher = keyboard.nextLine();
        ePublicationDate = keyboard.nextLine();
        edition = keyboard.next();
        numPages = keyboard.nextInt();

        myBook.setTitle(title);
        myBook.setAuthor(author);
        myBook.setPublisher(publisher);
        myBook.setPublicationDate(publicationDate);
        myBook.printInfo();

        myEncyclopedia.setTitle(eTitle);
        myEncyclopedia.setAuthor(eAuthor);
        myEncyclopedia.setPublisher(ePublisher);
        myEncyclopedia.setPublicationDate(ePublicationDate);
        myEncyclopedia.setEdition(edition);
        myEncyclopedia.setNumPages(numPages);
        myEncyclopedia.printInfo();

    }
}

```
![Screenshot 2025-03-16 195844](https://github.com/user-attachments/assets/5a94f040-ba61-42ab-8813-5fbd51facc56)
