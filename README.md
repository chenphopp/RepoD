# RepoD
Question

## 1. How did you test your pipelines?
I tested the pipelines directly on my Jenkins instance:
- For **PipelineB**: I confirmed that it cloned RepoA, generated the Doxygen config, produced HTML docs, and archived `doc.tar.gz`.
<img width="1893" height="490" alt="image" src="https://github.com/user-attachments/assets/bf8acf0e-b7fe-45ef-a419-82b38c44c8f8" />
<img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/f6b47d9b-31e1-485a-86fb-2d50da13d5f0" />

- For **PipelineC**: I verified that Doxygen produced `warnings.log`, then RepoC’s parser script successfully generated `warnings.csv`. Both were archived in Jenkins as artifacts.
<img width="1894" height="522" alt="image" src="https://github.com/user-attachments/assets/75c390a3-aa2f-49b5-8071-c05df373f616" />
<img width="460" height="305" alt="image" src="https://github.com/user-attachments/assets/4df4ec97-78ac-42f5-8ba0-ad40ed1dcfdb" />

## 2. How did you test RepoC Python?
- I first ran the parser locally with a sample `warnings.log` file produced by Doxygen.
- Verified that non-standard lines were ignored.
- Confirmed that the output CSV contained the expected columns: Line, File, Message.

<img width="1862" height="839" alt="image" src="https://github.com/user-attachments/assets/4be44070-259c-41fb-954f-5ee3243ceca1" />

## 3. What is the advantage to use LFS?
- Efficiently manages large binary files (e.g., .tar.gz, .zip, .exe).
- Stores only a pointer in the Git repo, so the repo size stays small.
- Faster clone/pull operations.
- Developers download only the needed file versions.

## 4. How to adjust this repository to support LFS?
- Install Git LFS (git lfs install) : https://git-lfs.com/
- Tracking the large binary
```
git lfs track "*.tar.gz"
git lfs track "*.zip"
git lfs track "*.exe"
```
```
git add .gitattributes
```
```
git commit -m "Enable Git LFS for large binaries"
git push origin main
```

Alternatives:
- Use Jenkins artifacts, Nexus, JFrog or Artifactory for binary storage instead of Git.

