# LEETCODE-Linked_List-3217
---

## 🧩 Code ka purpose:

Yeh function linked list ke **wo saare nodes hata deta hai**
jin ke values `nums` array me diye hue hain.

---

## 🧠 Example:

```java
nums = [1, 3, 5]
Linked List = 1 → 2 → 3 → 4 → 5 → 6
```

Goal:
Delete nodes with values 1, 3, 5
✅ Output linked list → `2 → 4 → 6`

---

## 🧱 Step-by-Step Dry Run

### Step 1️⃣ — Create the HashSet

```java
HashSet<Integer> st = new HashSet<>();
for(int num : nums) {
    st.add(num);
}
```

Now:

```
st = {1, 3, 5}
```

---

### Step 2️⃣ — Remove bad nodes from the beginning

```java
while (head != null && st.contains(head.val)) {
    head = head.next;
}
```

Dry run:

| Head value | In Set? | Action        |
| ---------- | ------- | ------------- |
| 1          | ✅ Yes   | Move head → 2 |
| 2          | ❌ No    | Stop loop     |

Now:

```
head = 2
```

✅ The new head is 2, because 1 was deleted.

List now looks like:

```
2 → 3 → 4 → 5 → 6
```

---

### Step 3️⃣ — Initialize pointers

```java
ListNode prev = null;
ListNode curr = head;
```

So:

```
prev = null
curr = 2
```

---

### Step 4️⃣ — Traverse the list

We start the main `while (curr != null)` loop.

---

#### 🔹Iteration 1:

```
curr = 2
st.contains(2)? ❌
```

➡ Keep this node.

So:

```
prev = curr  (prev = 2)
curr = curr.next  (curr = 3)
```

Pointers:

```
prev → 2 → 3 → 4 → 5 → 6
         ↑
        curr
```

---

#### 🔹Iteration 2:

```
curr = 3
st.contains(3)? ✅
```

➡ Delete this node.

`prev != null` → true (prev = 2)
So:

```java
prev.next = curr.next;  // 2 → 4
curr = curr.next;       // curr = 4
```

Updated list:

```
2 → 4 → 5 → 6
```

---

#### 🔹Iteration 3:

```
curr = 4
st.contains(4)? ❌
```

➡ Keep this node.

```java
prev = curr;  // prev = 4
curr = curr.next; // curr = 5
```

Pointers:

```
2 → 4 → 5 → 6
        ↑
       curr
```

---

#### 🔹Iteration 4:

```
curr = 5
st.contains(5)? ✅
```

➡ Delete this node.

`prev != null` → true (prev = 4)
So:

```java
prev.next = curr.next; // 4 → 6
curr = curr.next; // curr = 6
```

List becomes:

```
2 → 4 → 6
```

---

#### 🔹Iteration 5:

```
curr = 6
st.contains(6)? ❌
```

➡ Keep this node.

```java
prev = curr; // prev = 6
curr = curr.next; // curr = null
```

---

### Step 5️⃣ — Loop ends

`curr == null` → exit the loop.
Return the updated head.

✅ **Final Linked List:**

```
2 → 4 → 6
```

---

## 🔍 Summary Table

| Step | curr.val | In Set? | Action        | Updated List      |
| ---- | -------- | ------- | ------------- | ----------------- |
| 1    | 2        | ❌       | Keep (prev=2) | 2 → 3 → 4 → 5 → 6 |
| 2    | 3        | ✅       | Delete 3      | 2 → 4 → 5 → 6     |
| 3    | 4        | ❌       | Keep (prev=4) | 2 → 4 → 5 → 6     |
| 4    | 5        | ✅       | Delete 5      | 2 → 4 → 6         |
| 5    | 6        | ❌       | Keep (prev=6) | 2 → 4 → 6         |

✅ Final Output → `2 → 4 → 6`

---
