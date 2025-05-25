### Q. What is cold/warm/hot start?
**A**
| Launch type    | What the system must create / restore                                                                                                                                                       | Typical duration\* | Why it’s slower / faster                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Cold Start** | **Process** + Zygote fork → ClassLoader → `Application` object → `attachBaseContext()` → `Application.onCreate()` → **First `Activity`** (`onCreate → onStart → onResume`) + view inflation | 400 ms – 2 s       | Nothing is resident in RAM; all code & resources must be paged in, dependencies built, dex‑opt maps set up. |
| **Warm Start** | **Existing process** is still in memory → *Skip* Zygote fork & `Application` init → Create or restore target `Activity` (may still need `onCreate` if reclaimed)                            | 200 ms – 700 ms    | Process stays cached; OS just walks the back‑stack or launches a new activity instance inside the same VM.  |
| **Hot Start**  | Process + activity already live in back stack (e.g., user alt‑tabs back within seconds) → Only `onRestart → onStart → onResume`                                                             | < 100 ms           | Views already inflated; just resume and draw next frame.                                                    |



### Q. How do you optimize app startup?

### Q. Where do you initialize global dependencies?

### Q. What is the role of the Application class?

### Q. How do you measure and reduce TTI (Time to Interactive)?
