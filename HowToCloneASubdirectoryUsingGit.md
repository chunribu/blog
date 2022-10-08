[🏠HOME](./README.md)

# How to clone a subdirectory using git

---

```bash
git clone --filter=blob:none --sparse  %your-git-repo-url%
git sparse-checkout add %subdirectory-to-be-cloned%
```


**Explanation**

`--filter=blob:none`: You tell git that you only want to clone the metadata files. This way git collects the basic branch details and other meta from remote, which will ensure that your future checkouts from origin are smooth.

`--sparse`: Tell git that this is a sparse clone. Git will checkout only the root directory in this case.