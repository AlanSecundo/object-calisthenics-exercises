# Exercícios sobre Object Calisthenics

Um repositório simples com alguns exercícios básicos relacionados as boas práticas baseados no conceito de Object Calisthenics.

# Exercícios

## 1 - Only One Level Of Indentation Per Method

Exercício: Refatore um método complexo em uma classe de sistema bancário para garantir que cada método tenha apenas um nível de indentação.

```
public class BankAccount {
    private double balance;
    private List<String> transactionHistory;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
        this.transactionHistory = new ArrayList<>();
    }

    public void processTransactions(List<Transaction> transactions) {
        for (Transaction transaction : transactions) {
            if (transaction.getType().equals("deposit")) {
                if (transaction.getAmount() > 0) {
                    balance += transaction.getAmount();
                    transactionHistory.add("Deposited: " + transaction.getAmount());
                } else {
                    transactionHistory.add("Invalid deposit amount: " + transaction.getAmount());
                }
            } else if (transaction.getType().equals("withdraw")) {
                if (transaction.getAmount() > 0 && transaction.getAmount() <= balance) {
                    balance -= transaction.getAmount();
                    transactionHistory.add("Withdrew: " + transaction.getAmount());
                } else {
                    transactionHistory.add("Invalid withdrawal amount or insufficient funds: " + transaction.getAmount());
                }
            }
        }
    }
}
```

## 2 - Don’t Use The ELSE Keyword

Exercício: Refatore um método em uma aplicação de e-commerce para evitar o uso do ELSE.

```
public class Order {
    private double totalAmount;
    private String status;

    public void updateStatus(String paymentStatus, boolean inStock) {
        if (paymentStatus.equals("paid")) {
            if (inStock) {
                status = "confirmed";
                totalAmount *= 0.9; // Apply discount
            } else {
                status = "waiting for stock";
            }
        } else {
            status = "payment pending";
        }
    }

}
```

## 3 - Wrap All Primitives And Strings

Exercício: Crie uma aplicação de gerenciamento de biblioteca onde você deve encapsular todos os tipos primitivos e strings em classes específicas.

Requisitos:

Encapsule ISBN, Title e Author como classes.
Implemente métodos comportamentais específicos em vez de getters e setters diretos.

```
public class Library {
    private List<Book> books;

    public void addBook(String isbn, String title, String author) {
        books.add(new Book(isbn, title, author));
    }

    public void removeBook(String isbn) {
        books.removeIf(book -> book.getIsbn().equals(isbn));
    }

    // other methods
}

public class Book {
    private String isbn;
    private String title;
    private String author;

    public Book(String isbn, String title, String author) {
        this.isbn = isbn;
        this.title = title;
        this.author = author;
    }

    // getters and setters
}
```

## 4 - First Class Collections

Exercício: Encapsule uma coleção dentro de uma classe que ofereça operações específicas como addStudent e removeStudent.

```
public class Classroom {
    private List<Student> students;

    public List<Student> getStudents() {
        return students;
    }
}
```

## 5 - One Dot Per Line

Exercício: Refatore o código para garantir que cada linha tenha apenas uma chamada de método.

```
public void printStudentNames(Classroom classroom) {
    classroom.getStudents().forEach(student -> System.out.println(student.getName()));
}
```

## 6 - Don’t Abbreviate

Exercício: Refatore o código para usar nomes completos e descritivos.

```
public void calc(int num1, int num2) {
    int res = num1 + num2;
    System.out.println(res);
}
```

## 7 - Keep All Entities Small

Exercício: Reestruture uma aplicação de gerenciamento de projetos para que cada classe tenha uma única responsabilidade e mantenha-se pequena.

Requisitos:

Divida a classe Project em várias classes menores, cada uma responsável por uma única tarefa (e.g., Gerenciamento de Tarefas, Gerenciamento de Equipes, Relatórios).

```
public class Project {
    private String name;
    private List<String> teamMembers;
    private List<String> tasks;
    private Map<String, String> taskAssignments;

    public Project(String name) {
        this.name = name;
        this.teamMembers = new ArrayList<>();
        this.tasks = new ArrayList<>();
        this.taskAssignments = new HashMap<>();
    }

    public void addTeamMember(String member) {
        teamMembers.add(member);
    }

    public void addTask(String task) {
        tasks.add(task);
    }

    public void assignTask(String task, String member) {
        taskAssignments.put(task, member);
    }
}
```

## 8 - No Classes With More Than Two Instance Variables

Exercício: Refatore uma aplicação de reserva de hotel para que nenhuma classe tenha mais de duas variáveis de instância.

Requisitos:

- Divida a classe Booking em várias classes menores que cada uma tenha no máximo duas variáveis de instância.
- Utilize composição para gerenciar os dados de reserva, cliente e pagamento.

```
public class Booking {
    private String bookingId;
    private String customerName;
    private String customerEmail;
    private double amountPaid;
    private String paymentMethod;

    public Booking(String bookingId, String customerName, String customerEmail, double amountPaid, String paymentMethod) {
        this.bookingId = bookingId;
        this.customerName = customerName;
        this.customerEmail = customerEmail;
        this.amountPaid = amountPaid;
        this.paymentMethod = paymentMethod;
    }
}
```

## 9 - No Getters/Setters/Properties

Exercício: Remova getters e setters diretos, usando métodos comportamentais em vez disso.

Sugestão de métodos comportamentais:

- haveBirthday();
- rename(String newName);

```
public class Person {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
