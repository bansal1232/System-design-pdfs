# 🚀 High-Impact Low-Level Code Optimizations

This repo showcases real-world code-level optimizations that may look small — but create **huge performance impacts**, especially in games, system design, graphics, and high-scale applications.

---

## 1. 🎮 Fast Inverse Square Root (Quake III)
```c
float InvSqrt(float x) {
    float xhalf = 0.5f * x;
    int i = *(int*)&x;
    i = 0x5f3759df - (i >> 1);
    x = *(float*)&i;
    x = x * (1.5f - xhalf * x * x);
    return x;
}
```
✅ Used for real-time lighting calculations in 3D games. Gave a massive FPS boost on old CPUs.

---

## 2. 🧮 Doom Fixed-Point Math
```c
#define FRACBITS 16
#define FRACUNIT (1 << FRACBITS)

int FixedMul(int a, int b) {
    return (int)(((long long)a * b) >> FRACBITS);
}
```
✅ Used by Doom to replace floating-point operations with faster fixed-point math.

---

## 3. 🧹 Object Pooling (e.g., NES Games like Mario)
```c
// Reuse objects instead of dynamic allocation
Enemy enemies[10];
for (int i = 0; i < 10; i++) {
    if (!enemies[i].isActive) {
        spawnEnemy(&enemies[i]);
        break;
    }
}
```
✅ Reduces memory fragmentation and allocation cost.

---

## 4. ⚡ Bitmask Flags for Game Object State
```c
#define IS_VISIBLE 0x01
#define IS_LIT     0x02

uint32_t flags = 0;
flags |= IS_VISIBLE;

if (flags & IS_VISIBLE) {
    // Draw object
}
```
✅ Super-fast state checking and less memory use.

---

## 5. 🧊 Greedy Meshing in Minecraft
```js
// Instead of rendering every face individually,
// combine adjacent similar faces into one large quad.
```
✅ Reduced draw calls and vertex count significantly — massive FPS gains.

---

## 6. 🧠 Memoization (Fibonacci Example)
```js
const cache = {};
function fib(n) {
  if (n in cache) return cache[n];
  if (n <= 1) return n;
  return cache[n] = fib(n - 1) + fib(n - 2);
}
```
✅ Turns exponential recursion into linear time.

---

## 7. 🔢 XOR Swap
```c
int a = 5, b = 3;
a = a ^ b;
b = a ^ b;
a = a ^ b;
```
✅ Swap values without temp variable. Cool trick, rarely used in modern code.

---

## 8. 🔍 Set Lookup vs Array Includes (JS)
```js
const arr = [1, 2, 3, 4];
arr.includes(3); // O(n)

const set = new Set(arr);
set.has(3); // O(1)
```
✅ Huge gain when checking inside large collections.

---

## 9. 🧪 Lazy DOM Manipulation (Web)
```js
// Avoid reflow by batching style changes:
element.style.cssText = "width: 100px; height: 100px; background: red;";
```
✅ Faster UI rendering with fewer reflows/repaints.

---

## 10. 🧬 String Interning (Java/Python)
```java
String s1 = "hello";
String s2 = "hello";
s1 == s2; // true due to interning
```
✅ Faster string comparisons, lower memory use.

---

## 11. 🧵 Kernel Optimizations: Avoid Function Calls in Hot Paths
```c
#define LIKELY(x)   __builtin_expect(!!(x), 1)
#define UNLIKELY(x) __builtin_expect(!!(x), 0)

if (LIKELY(condition)) {
  fast_path();
} else {
  slow_path();
}
```
✅ Used in Linux kernel to reduce branch mispredictions.

---

## Contributions
Feel free to add more low-level or clever optimization examples!

---

## License
MIT
