Typscript yeni bir dil değildir. Javascript’e ek bazı özellikler verilerek uzantı bir dil oluşturulmuştur. Javascript oop özelliklerini taşımadığı için diğer dillere nazaran bazı konularda yetersiz kalmıştır. Benim fikrime göre Typescript, avascriptin oop halidir.

Statik bir dil olduğu için js ‘ e bakınca avantajı vardır. Ts hatayı compile aşamasında verir, js ise runtime sırasında verir. Böylece hataları daha erken fark etmemizi sağlar.

Typescript model-view-controller(mvc) prensibine benzediği için büyük projelerde uygulama yönetmek daha kolaydır.

Vs kodda typescript projr oluşturmak için terminalden,

**_npm i -g typescript_** yazmamız gerekiyor.

ts dosyaları bilgisayar tarafından okunamadığı için kodun js dosyasına dönüşmesü gerekir. Bunun için powershell’e **_tsc “dosyaadı”_** şeklinde yazmamız gerekiyor. Bu sayede ts dosyası, js dosyasına dönüşür.

consol.log kullanarak çıktı almak istediğimiz ts kodunu js koduna çevirdikten sonra, poweshell’e **_node “dosyaadı.js”_** şeklinde yazabiliriz. Aynı şekilde bunu web browser da yazdırmak isteseydik

index.html dosyaysına script taglari arasında src’de dosyanın yolunu yazardık.

Stackblitz’i kullan!!

### Type değişimleri:

Infrence sayesinde, typescript eğer değeri ilk başta tipini tanımlamadan verdiysen tipini anlar.

**Array:**

```tsx
let myArray: string[];
myArray = ["a", "b", "c"];
```

**Enum:**

```tsx
enum Color {
  Blue,
  Black,
  Purple,
}
let bgColor = Color.Blue;
```

**Tuple:**

Eğer alimizde sayısı ve tipleri belli olan bir array varsa kullanırız

```tsx
let error = [string, number];
error = ["not found", 404];
```

**Any ve Unknown arasındaki fark:**

Any tipi değişkene eğer herhangi bir tipte değer atamak istersek kullanırız. unknown veri tipinde ise bilmediğimiz veri tipinde kullanırız. Bilmediğimiz veri tipi number string veya array olabilir. Any’den farkı, eğer ben _let a= 4;_ diye bir tanım yapmışsam ve bunu l*et x; a=x*; diye atayailirim. Ama aynısını unknown tipinde yapamam.

### Type Assertion

eğer ben any tipli bir değişken oluşturduysam ve daha sonra bunun bir string olduğuna karar verdiysem, tip ddönüşümünü aşağıdaki gibi yaparım.

```tsx
let message;
message = "Didem";

const newMessage = (<string>message).toLowerCase();
//yada
const newMessage = (message as string).toLoweCase();
```

Eğer yukarıdaki kodda ben mesaja string dediysem ve mesaj number ise hata alırız. Çünkü typescript tür dönüşümü yapmaz.

**Object Type:**

```tsx
let user = {
  id: 1,
  name: "Gül",
  age: 26,
};

//yada

let user: {
  id: number;
  name: string;
  age: number | string; //Union type: iki değeri de kabul ettiği anlamına gelir.
  role: "admin"; //Literal type. Typescript type değil kendimi belirleriz
};

user = {
  id: 1,
  name: "Gülderen",
  age: 26,
};

user.id; //örneğin
```

**Custom Type:**

Eğer ben kendim bir type oluşturmak istersem;

```tsx
type Color = {
  name: string;
  hex: string;
};

let user: {
  id: number;
  name: string;
  age: number | string; //Union type: iki değeri de kabul ettiği anlamına gelir.
  role: "admin";
  color: Color;
};
user.color.name = "purple";
```

**Union Type:**

```tsx

```

### Fonksiyon:

```tsx
const add = (num1: number, num2: number) => {
  return num1 + num2;
};
add(2, 3);
```

Eğer functin içindeki bir değerin gelip gelmediğinden emin değilsem,

```tsx
const logUser = (name: string, surname?: string) => {
  //surname'in yanına soru işareti koyarım
  console.log(name + " " + surname);
};
logUser("Gülderen");
```

### Interface:

```tsx
interface Person {
	name:string;
	age: number;
}

inteface Employee extends Person {
	readonly empId: number //değeri değiştirilemez
}

let newEmployee : Employee;

newEmployee = {
	name: "Gül",
	age: 26,
	empId:1,
};
```

### Implementing Interface:

```tsx
interface IEmployee {
  name: string;
  age: number;
  empID: number;
  getSalary: (number) => number;
}

class Employee implements IEmployee {
  name: string;
  age: number;
  empID: number;

  constructor(name: string, age: number, empID: number) {}

  getSalary = (empID: number) => {
    return 10000;
  };
}
let newEmployee = new Employee("Gül", 25, 1);
console.log(newEmployee.age);
```

We can define object like that;

```tsx
let myCar = ["Toyota", "Corolla", 2002];

const [make, model, year] = myCar;
```

On the above code we can see how to use tuple type. If I write like that,

```tsx
let myCar = [2002, "Toyota", "Corolla"];
```

It will be getting error because on the previous code, we defined this array string-string-number.

But this code’s placement is different than its defines.

**Pop-push problem:**

There is an thing still havent solve from typescript. When I define a tuple array I can’t change but if I use push or pop method.

```tsx
const numPair: [number, number] = [2, 3];
numPair.push(4); //[2,3,4]
numPair.pop(); // [2,3]
numPair.pop(); //[2]
```
