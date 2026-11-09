# Tech Stack Evaluation

## Project
Predicting UiTM e-course registration demand so server capacity can scale
up before the peak week and the system stops hanging or crashing.

## Requirements that drive the decision
- FR-1: The system shall forecast registration demand for the announced registration week.
- FR-2: The system shall increase server capacity before the forecast peak and reduce it afterwards.
- NFR-1: The registration page must stay reachable during peak registration (availability).
- NFR-2: The page must respond within an acceptable time under peak load (performance).
- NFR-3: Running cost outside the peak week must stay low (cost).

## Options
- Option A: Static dashboard (HTML and JavaScript) on GitHub Pages, with forecasts calculated offline.
- Option B: Python web app (Flask or FastAPI) with a forecasting model and a database on a cloud host with autoscaling.
- Option C: Fully managed serverless cloud (functions, managed database, scheduled forecasting job).

## Decision matrix
Weight: how important the criterion is for YOUR project (1 = low, 5 = high).
Score: how well each option does (1 = poor, 5 = excellent).
Weighted score = weight x score. Add them up for each option.

| Criterion                          | Weight | A score | B score | C score |
|------------------------------------|--------|---------|---------|---------|
| Fits my requirements               | 5      | 2       | 5       | 4       |
| Skills I already have              | 4      | 5       | 4       | 2       |
| Time to build before my deadline   | 4      | 5       | 3       | 2       |
| Free hosting and tools             | 3      | 5       | 3       | 3       |
| Performance and security needs     | 5      | 2       | 4       | 5       |
| Room to grow later                 | 3      | 1       | 4       | 5       |
| **Total (weighted)**               |        | **78**  | **94**  | **85**  |

## Decision record
- **Context:** Registration traffic spikes in a known week each semester and
  the site becomes unreachable. I have limited time and mostly Python skills,
  and I want low cost outside the peak week.
- **Decision:** Option B, a Python web app with a forecasting model and a
  database on an autoscaling cloud host.
- **Reasons:** (1) The forecasting requirement needs a Python ML library,
  which a static site cannot run (Fits my requirements). (2) The availability
  and performance NFRs need autoscaling, which B provides and A cannot.
  (3) B scored highest overall (94 vs 85 and 78) and I already know Python.
- **Consequences:** Easy: using Python libraries for time-series forecasting
  and scaling only when needed. Harder: I must set up and maintain the server,
  database and scaling rules, and watch the cost.
- **Risks and next review:** Little historical data could make the forecast
  inaccurate. My decision would change to Option C if I had more cloud
  experience or free-tier limits were exceeded, and to Option A if only a
  demo dashboard was needed. Review again before the final report.