## 835. Image Overlap

🔗 https://leetcode.com/problems/image-overlap/

---

## 🧩 Problem

You are given two images, `img1` and `img2`, both represented as binary, square matrices of size `n x n`. A binary matrix has only `0`s and `1`s as values.

We **translate** one image however we choose by sliding all the `1` bits left, right, up, and/or down any number of units. We then place it on top of the other image. We can then calculate the **overlap** by counting the number of positions that have a `1` in **both** images.

Note also that a translation does **not** include any kind of rotation. Any `1` bits that are translated outside of the matrix borders are erased.

Return the largest possible overlap.

---

## 📌 Examples

### Example 1:

**Input:**

```python
img1 = [[1,1,0],[0,1,0],[0,1,0]]
img2 = [[0,0,0],[0,1,1],[0,0,1]]
```

**Output:**

```python
3
```

**Explanation:**

We translate `img1` to the right by 1 unit and down by 1 unit. The number of positions that have a `1` in both images is 3.

---

### Example 2:

**Input:**

```python
img1 = [[1]]
img2 = [[1]]
```

**Output:**

```python
1
```

---

### Example 3:

**Input:**

```python
img1 = [[0]]
img2 = [[0]]
```

**Output:**

```python
0
```

---

## 🔒 Constraints

* `n == img1.length == img1[i].length`
* `n == img2.length == img2[i].length`
* `1 <= n <= 30`
* `img1[i][j]` is either `0` or `1`
* `img2[i][j]` is either `0` or `1`

---

## 💡 Approach (Brute Force over Translations)

* Collect the coordinates of every `1` in `img1` into a list `r`
* Build all possible translation vectors `(i, j)` where both `i` and `j` range from `-(n-1)` to `n-1`
* For each translation:
  * Shift every `1` in `r` by `(i, j)`
  * If the shifted cell lies inside the grid and `img2` has a `1` there, increase the count
* Track the maximum count across all translations and return it

---

## ⏱ Complexity

* **Time Complexity:** `O(n^4)` → `(2n-1)^2` translations × up to `n^2` ones
* **Space Complexity:** `O(n^2)` → stores the translations and the coordinates of ones

---

## 🧠 Solution (Python)

```python
class Solution:
    def largestOverlap(self, img1: list[list[int]], img2: list[list[int]]) -> int:
        n = len(img1)
        d = [[a, b] for a in range(-(n - 1), n) for b in range(-(n - 1), n)]
        r=[]
        res=0

        for i in range(len(img1)):
            for j in range(len(img1)):
                if img1[i][j]==1:
                    r.append([i,j])

        for i, j  in d:
            count=0

            for x,y in r:
                nr=i+x
                nc=j+y

                if 0<=nr<len(img1) and 0<=nc<len(img2):
                    if img2[nr][nc]==1:
                        count+=1

            res=max(res,count)


        return res
```
