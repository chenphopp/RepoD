<img width="1884" height="661" alt="image" src="https://github.com/user-attachments/assets/dd3be212-e3da-4b00-8f14-43ebc30a678f" /># RepoD
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

