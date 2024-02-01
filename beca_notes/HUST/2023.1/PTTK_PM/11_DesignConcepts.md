![[11_DesignConcepts-20231205054115479.webp]]
*(Design levels)*
> [!abstract] Key design concepts
> * **Cohesion**
> * **Coupling**
> * Information hiding (Encapsulation, Creation)

> [!check] Mục tiêu
> Loose Coupling - High cohension

## 1. Coupling
![[11_DesignConcepts-20231205162612541.webp|514]]
### 1.1 Content Coupling
* Vi phạm coupling ở mức cao nhất
* Khi một component có thể truy cập **trực tiếp** vào hoạt động bên trong của 1 component
	* Trực tiếp truy xuất data
	* Trực tiếp thay đổi data của component

Ex
```java
class BankAccount{
	private balance;
	// should not use
	public void setBalance();

	// -> Do this instead
	public void deleteBalance(params);
}
```
![[11_DesignConcepts-20231205164348270.webp]]

### 1.2 Common Coupling
* Hai hay nhiều module cùng đọc và thay đổi 1 dữ liệu dùng chung.
```java
public class GlobalData {
    public static int sharedData;
}

public class ModuleA {
    public void methodA() {
        GlobalData.sharedData = 5;
    }
}

public class ModuleB {
    public void methodB() {
        int data = GlobalData.sharedData;
    }
}
```

-> Improve:
```java
public class SharedData {
    private int data;

    public int getData() {
        return data;
    }

    public void setData(int data) {
        this.data = data;
    }
	}

public class ModuleA {
    private SharedData sharedData;

    public ModuleA(SharedData sharedData) {
    // pass reference
        this.sharedData = sharedData;
    }

    public void methodA() {
        sharedData.setData(5);
    }
}

public class ModuleB {
    private SharedData sharedData;

    public ModuleB(SharedData sharedData) {
    // pass reference
        this.sharedData = sharedData;
    }

    public void methodB() {
        int data = sharedData.getData();
    }
}
```

### 1.3 Control Coupling
* xảy ra khi tham số truyền vào module sẽ quyết định luồng xử lý của module theo những cách khác nhau.

* Khi một phương thức sẽ quyết định luồng xử lý dữ liệu của phương thức khác bằng cách truyền cho nó tham số để điều khiển.

Ex:
```java
public class MediaRepo {
    public List<? extends Media> findMedia(String mediaCategory, String name, boolean all) {
        if (all) {
            return findAllMedias();
        } else {
            switch (mediaCategory) {
                case "Book":
                    return findBooksFilterByTitle(name);
                case "DVD":
                    return findDVDsFilterByTitle(name);
                case "CD":
                    return findCDsFilterByTitle(name);
                default:
                    return new ArrayList<>();
            }
        }
    }
}

public class MediaService {
    private MediaRepo mediaRepo;

    public MediaService(MediaRepo mediaRepo) {
        this.mediaRepo = mediaRepo;
    }

    public List<? extends Media> getMediaByCategoryAndName(String mediaCategory, String name, boolean all) {
        return mediaRepo.findMedia(mediaCategory, name, all);
        // tham số all được truyền vào 
        // -> func ở MediaService quyết định hướng hành động của func ở MediaRepo
    }
}
```

> [!check] Những cách để tránh control coupling
> 1. **Polymorphism**: Use interfaces and abstract classes to define common methods, and let each class implement them in their own way. This way, you can pass around interfaces or abstract classes instead of concrete classes, reducing the dependency on specific behaviors.
> 2. **Dependency Injection**: Instead of having a class create its own dependencies or control their behavior, pass the dependencies into the class. This can be done through the constructor (constructor injection) or through setter methods (setter injection).

### 1.4 Stamp Coupling
> Data are passed by parameters using a data structure containing fields which may or may not be used.

* cần tới thành phần thứ hai biết cách thao tác với data structure
* Có thể cần thiết vì yếu tố tối ưu
* Coupling ở mức độ có thể chấp nhận được👍

Ex:
The print routine of the customer billing accepts a customer data structure as an argument, and prints the name, address and billing information

-> Improve: the print routine takes the customer name, address and billing information as an argument.

### 1.5 Data Coupling
> Two components are data coupled if there are homogeneous (đồng nhất) data items.

* Modules share data through parameters, and only data is shared.
* Là mức thấp nhất, khi mà các modules tương tác với nhau chỉ thông qua tham số truyền vào

![[11_DesignConcepts-20240130232247076.webp|468]]


## 2. Cohension
![[11_DesignConcepts-20231205174656991.webp]]

### 2.1 Coincidental cohension
* Ko liên quan gì đến mục tiêu thể hiện của component

![[11_DesignConcepts-20240130230430943.webp|208]]

### 2.2 Logical cohension
* Khi các components liên quan đến nhau theo logic chứ không phải liên quan với nhau theo chức năng
VD:
* Các functions đọc dữ liệu đầu vào từ tape, disk hay network cùng ở chung 1 module nghe có vẻ hợp lý và vì chúng liên quan đến nhau đó là xử lý dữ liệu đầu vào nhưng rõ ràng chức năng của chúng là khác nhau hoàn toàn.
-> Tạo 1 interface có method là readInput() để các sub-class implement đến override lại mothod readInput(). Sub-class Tape sẽ đọc từ tape, sub-class disk sẽ đọc từ disk, và tương tự với network mà với những chức năng đọc từ nguồn khác cũng được mở rộng tương tự.

![[11_DesignConcepts-20240130235715171.webp|258]]

### 2.3 Temporal cohension
* Những elements liên quan đến nhau theo thời gian chứ không theo chức năng và những elements này được thực thi gần như trong cùng một khoảng thời gian

Ex:
![[11_DesignConcepts-20231205175505146.webp]]

![[11_DesignConcepts-20240130235734710.webp|217]]

### 2.4 Procedural cohension
* Những elements liên quan đến nhau chỉ để đảm bảo một thứ tự thực thi cụ thể.

![[11_DesignConcepts-20240130235809955.webp|310]]

Ex:
```c
Class Student
    Method CalculateSemesterGPA
        // Calculate the average GPA for the semester
        semesterGPA = Sum of all grades for the semester / Number of courses in the semester
        return semesterGPA

    Method SaveSemesterGPA
        // Save the semester GPA to the database
        Call database API to save semesterGPA

    Method CalculateCumulativeGPA
        // Calculate the cumulative GPA for all semesters
        cumulativeGPA = Sum of all semesterGPAs / Number of semesters
        return cumulativeGPA

    Method SaveCumulativeGPA
        // Save the cumulative GPA to the database
        Call database API to save cumulativeGPA

    Method UpdateGPAs
        // Calculate and save the semester and cumulative GPAs
        semesterGPA = CalculateSemesterGPA()
        SaveSemesterGPA(semesterGPA)
        cumulativeGPA = CalculateCumulativeGPA()
        SaveCumulativeGPA(cumulativeGPA)
End Class
```

### 2.5 Communication Cohension
* Là một nhóm các elements của module cùng hoạt động trên cùng một data là dữ liệu I/O của các methods.

![[11_DesignConcepts-20240130235834771.webp]]

### 2.6 Sequential Cohension
* Khi output của một element trở thành input của một element khác
![[11_DesignConcepts-20231205180837927.webp]]

### 2.7 Informational Cohension
> Module performs a number of actions, each with its own entry point, with independent code for each action, all performed on *the same data*

* Different from logical cohension
	* Each piece of code has single entry and single exit
	* In logical cohension, actions of module intertwined
### 2.8 Functional Cohension
> Every element in the component are essential to the computation

* Ideal Situation
![[11_DesignConcepts-20240130235906326.webp]]

