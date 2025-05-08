# 🎯 TypeScript Interview Blog

## 1. What are some differences between interfaces and types in TypeScript?

TypeScript-এ `interface` এবং `type` অনেকটা একই রকম মনে হলেও, কিছু গুরুত্বপূর্ণ পার্থক্য রয়েছে।

### 🔹 ১. Use

- **`interface`**: মূলত object-এর shape বা কাঠামো বর্ণনা করতে ব্যবহৃত হয়।
- **`type`**: শুধু object না, যেকোনো ধরনের টাইপ (primitive, union, intersection, tuple ইত্যাদি) define করতে পারে।

### 🔹 ২. Extending

- **`interface`**:

```ts
interface A {
  name: string;
}

interface B extends A {
  age: number;
}
```

- **`type`**:

```ts
type A = {
  name: string;
};

type B = A & {
  age: number;
};
```

- দুইটাতেই inheritance করা যায়, কিন্তু `interface`-এ extends এবং `type`-এ & (intersection) দিয়ে করা হয়।

### 🔹 ৩. Redeclaration

- `interface`: একাধিকবার একই interface ঘোষণা করে properties বাড়ানো যায়।

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

// Final User = { name: string; age: number }
```

- `type`: একবার type ঘোষণা করলে, পুনরায় একই নামে declare করা যায় না।

```ts
type User = {
  name: string;
};

// Error
type User = {
  age: number;
};
```

### 🔹 ৪. Utility Type Compatibility

- `type` এবং `interface`—দুইটিতেই utility টাইপ ব্যবহার করা যায়, তবে type দিয়ে complex টাইপ composition সহজ হয়।

---

## 2. What is the use of the keyof keyword in TypeScript? Provide an example.

TypeScript-এ `keyof` একটি type operator, যা কোনো object টাইপের সব key (প্রপার্টির নাম) কে একটি string literal union টাইপ হিসেবে রিটার্ন করে।

### 🔹 Why is it used?

- একটি অবজেক্ট টাইপের ভ্যালিড key গুলো ধরে রাখতে বা validate করতে।
- জেনেরিক ফাংশন/টাইপ তৈরির সময় টাইপকে আরও type-safe ও ডাইনামিক করার জন্য।

### 🔹Syntax

```ts
keyof Type
```

### 🔹Example

```ts
type Person = {
  name: string;
  age: number;
  email: string;
};

type PersonKeys = keyof Person;
// PersonKeys এখন "name" | "age" | "email"
```

- এখানে keyof Person টাইপটি Person অবজেক্টের সব কীগুলোকে (key name) একটি ইউনিয়ন টাইপ হিসেবে রিটার্ন করেছে।
