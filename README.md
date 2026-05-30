# Unity C# Unit Testing — Matrix Library

A Unity project demonstrating how to write and run unit tests in C# using the **Unity Test Framework** (NUnit). The subject under test is a custom `Matrix` class that implements basic linear algebra operations.

## Project Structure

```
Assets/
├── Scripts/
│   ├── Matrix.cs              # Core Matrix class (MyLinearAlgebra assembly)
│   └── MyLinearAlgebra.asmdef
└── EditorTests/
    ├── MatrixConstructorsTests.cs   # 3 constructor tests
    ├── MatrixGettersTests.cs        # 3 property tests
    ├── MatrixOperatorsTests.cs      # 9 operator tests
    └── EditorTests.asmdef
```

## Matrix Class

`Matrix` is a general-purpose `m × n` matrix of `float` values.

### Constructors

| Signature | Description |
|-----------|-------------|
| `Matrix(float[,] coefficients)` | Initialize from a 2D array |
| `Matrix(int m, int n)` | Create an `m × n` zero matrix |
| `Matrix(Matrix a)` | Deep copy of an existing matrix |

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `Rows` | `int` | Number of rows |
| `Cols` | `int` | Number of columns |
| `NCoeffs` | `int` | Total element count (`Rows × Cols`) |

### Indexer

```csharp
float value = matrix[row, col];
matrix[row, col] = 3.14f;
```

### Operators

| Operator | Description |
|----------|-------------|
| `+a` | Returns a copy |
| `-a` | Element-wise negation |
| `a + b` | Element-wise addition (requires same size) |
| `a - b` | Element-wise subtraction (requires same size) |
| `f * a` / `a * f` | Scalar multiplication |
| `a * b` | Matrix multiplication (requires `a.Cols == b.Rows`) |

Size mismatches throw `InvalidOperationException` with a descriptive message.

## Unit Tests

Tests run inside the **Unity Editor** via **Window → General → Test Runner**.

| Test file | Cases | What is covered |
|-----------|-------|-----------------|
| `MatrixConstructorsTests` | 3 | All three constructors, deep-copy isolation |
| `MatrixGettersTests` | 3 | `Rows`, `Cols`, `NCoeffs` |
| `MatrixOperatorsTests` | 9 | Unary `-`, `+`, `-`, scalar `*`, matrix `*`, error paths |

## Requirements

- Unity **2020.3.18f1** (LTS)
- Unity Test Framework package (included via `Packages/manifest.json`)

## Running the Tests

1. Open the project in Unity 2020.3.
2. Go to **Window → General → Test Runner**.
3. Select the **EditMode** tab.
4. Click **Run All**.

## CI

A GitHub Actions workflow (`.github/workflows/activation.yml`) handles Unity license activation using [GameCI](https://game.ci/). It is triggered manually via `workflow_dispatch`.
