# FibMatrix-Android
Android Repo for the FibMatrix App

# 🧮 FibMatrix: An Android Application for O(log n) Fibonacci Computation

**FibMatrix** is a contemporary Android application, developed exclusively with **Jetpack Compose**, which functions as an interactive, visual compendium for mastering the **O(log n)** matrix exponentiation algorithm used for calculating Fibonacci numbers.

This application is engineered not merely as a utility, but as an **educational resource** to facilitate a deeper comprehension among students and engineers regarding the rationale and implementation of this powerful and prevalent technical interview algorithm.

---

## 📱 Application Demonstration

> 💡 _It is highly recommended to insert an animated GIF (10–15 seconds) here, demonstrating the application's core functionalities, such as theoretical exploration, sandbox computation, and dynamic chart updates._

---

## ✨ Core Features

### 🎓 Interactive Theoretical Module

A comprehensive, step-by-step guide articulating the mathematical principles behind the pivotal matrix:

<p align="center">
<pre>
| 1  1 |
| 1  0 |
</pre>
</p>

### 🧮 Computational Sandbox

The application's central utility. Users may input any integer `n` to instantly compute:

- The Fibonacci number `F(n)`
- The final matrix `Mⁿ`
- A comparative visualization of **O(n)** vs **O(log n)** computational complexity

### 🔬 O(log n) Recursion Trace

A visual tracer for the `power(M, n)` function, designed to elucidate the **exponentiation by squaring** methodology.

### 📊 Dynamic Complexity Chart

An interactive bar chart, rendered via the **Vico** library, quantitatively illustrating the performance disparity between the two algorithmic approaches.

### 💻 Algorithm-Source Display

A syntax-highlighted presentation of the complete Java algorithm, formatted for readability.

### 🌗 Dual-Theme UI

Implemented with **Material 3** components, featuring a polished, responsive interface that adapts to light and dark themes.

---

## 🛠️ Architecture & Technical Implementation

This project demonstrates **modern Android development best practices**, featuring a clean and scalable software architecture.

### 1. Architecture: Model–View–ViewModel (MVVM)

**ViewModel (`FibonacciViewModel.kt`)**  
Encapsulates all business logic, computation, and state management. Validates user input (e.g., ensuring numerical range safety) for application stability.

**View (`screens/*.kt`)**  
Stateless `@Composable` functions organized as screens. They observe state from the ViewModel and communicate user actions via a `UiEvent` system (e.g., `SandboxCalculate`).

**Model (`UiState.kt`)**  
A single immutable `UiState` data class represents the complete application state, managed via a `StateFlow`.

---

### 2. UI: Declarative Interface with Jetpack Compose

- **Fully Declarative:** The UI is built entirely with **Jetpack Compose**, including navigation and matrix visualizations.
- **Material 3:** Adheres to the latest Material Design 3 guidelines for components, color systems, and typography (`theme/Theme.kt`).
- **Custom Layouts:** `MatrixDisplay` and `VectorDisplay` composables manage complex, dynamic data layouts with proper alignment and scrollable overflow using a custom `EquationBox`.
- **State-Driven Recomposition:** Efficient recomposition occurs only when `UiState` changes.

---

### 3. State Management

- **Unidirectional Data Flow (UDF):**  
  State flows downward (ViewModel → UI) and events propagate upward (UI → ViewModel).
- **StateFlow:**  
  A private `MutableStateFlow` manages the internal state, exposed as immutable `StateFlow<UiState>` for UI consumption.
- **UiEvent Sealed Class:**  
  Defines all user interactions as discrete events, ensuring traceability and a clean ViewModel API.

---

### 4. Navigation

The app uses `androidx.navigation:navigation-compose` within a **Single-Activity** architecture.

**`AppNavigation.kt`:**  
A centralized `NavHost` component manages all screen transitions and navigational logic.

---

### 5. Third-Party Library Integration

- **Vico (Charting):** Demonstrates integration and customization of the [Vico charting library](https://github.com/patrykandpatryk/vico).  
  Includes a custom `ChartDisplay` composable with:
  - Custom axis labels (_O(n)_ vs _O(log n)_)
  - Integer-only Y-axis formatting
  - Persistent data labels for each bar

---

## 💡 Algorithmic Foundation: Matrix Exponentiation

The application's core logic is based on the following matrix identity:

<p align="center">
<pre>
| F(n+1) |   =   | 1  1 | × | F(n)   |
|  F(n)  |       | 1  0 |   | F(n−1) |
</pre>
</p>

This relationship can be extended through induction to yield:

<p align="center">
<pre>
| F(n)   |   =   | 1  1 |^(n−1) × | F(1) |
| F(n−1) |       | 1  0 |         | F(0) |
</pre>
</p>

Consequently, `F(n)` can be determined by computing the `(n−1)`th power of the matrix:

<p align="center">
<pre>
M = | 1  1 |
    | 1  0 |
</pre>
</p>

A naive approach would require `n−1` multiplications (**O(n)** time).  
This app implements **exponentiation by squaring**, reducing it to **O(log n)** time.  
The algorithm uses `BigInteger` to handle large Fibonacci values.

---

## 🚀 Key Dependencies

- [Jetpack Compose](https://developer.android.com/jetpack/compose) (BOM, UI, Material 3, Foundation)
- [Compose Navigation](https://developer.android.com/jetpack/compose/navigation)
- [Lifecycle ViewModel (Compose)](https://developer.android.com/topic/libraries/architecture/viewmodel)
- [Vico (Charting)](https://github.com/patrykandpatryk/vico)
- [Kotlin Coroutines](https://kotlinlang.org/docs/coroutines-overview.html) (for `StateFlow`)

---

## ⚙️ Build Instructions

1. Clone the repository.
2. Open the project directory in **Android Studio** (latest stable version).
3. Allow Gradle synchronization to complete.
4. Build and deploy to an emulator or physical device.

---

## 📄 License

```text
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
