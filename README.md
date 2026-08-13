<img src="https://capsule-render.vercel.app/api?type=waving&color=0:092E20,50:0F5132,100:2EAD33&height=180&section=header&text=Cau%C3%A3%20De%20Martin&fontColor=ffffff&fontSize=48&fontAlignY=34&desc=Backend%20Engineer%20%C2%B7%20Python%20%C2%B7%20Django%20%C2%B7%20Computer%20Vision&descAlignY=54&descSize=16&animation=fadeIn" width="100%" alt="Cauã De Martin — Backend Engineer">

<div align="center">

<a href="https://github.com/DeMart1n"><img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=22&duration=2800&pause=900&color=2EAD33&center=true&vCenter=true&width=560&lines=Multi-tenant+systems+in+production;Signal+processing+%26+pose+estimation;Django+%2B+DRF+%2B+Celery+at+scale;I+delete+more+code+than+I+write" alt="What I do"></a>

<br>

<img src="https://img.shields.io/badge/Varginha,%20MG%20—%20Brazil-092E20?style=for-the-badge&logo=googlemaps&logoColor=2EAD33" alt="Location">
<a href="mailto:cauademartin@gmail.com"><img src="https://img.shields.io/badge/Email-092E20?style=for-the-badge&logo=gmail&logoColor=2EAD33" alt="Email"></a>
<img src="https://komarev.com/ghpvc/?username=DeMart1n&style=for-the-badge&color=092E20&label=PROFILE+VIEWS" alt="Profile views">

</div>

---

I build production systems where the input is untrusted, the data can't leak, and the domain has more rules than a CRUD can hold. Two fronts that look unrelated and demand the same thing: **international logistics** and **motion analysis from computer vision**.

<div align="center">

<img src="https://skillicons.dev/icons?i=python,django,fastapi,postgres,redis,docker,aws,nginx,git,linux,js,bootstrap,go,swift,java,kotlin&perline=8" alt="Stack">

</div>

---

## Work

<table>
<tr>
<td width="50%" valign="top">

### Cargo Tracking Platform
`private` · Django · PostgreSQL · AWS

Multi-tenant platform for coffee export logistics. Multi-step wizards with dozens of inline formsets, per-company isolation enforced across models, views and forms, and resilient scraping pipelines replacing spreadsheets.

`multi-tenancy` `formtools` `pg_trgm` `ecs`

</td>
<td width="50%" valign="top">

### Motion Analysis Backend
`private` · DRF · Celery · YOLO Pose

Student records a set on their phone, on-device YOLO Pose extracts keypoints, the server scores execution against a reference template. ~170 routes, JWT/Argon2, Celery + Redis, Stripe Connect.

`dtw` `savitzky-golay` `signal-processing` `stripe`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [CRC](https://github.com/DeMart1n/CRC)
`public` · Swift

Control your Mac with hand gestures through the camera. Fully native — AVFoundation + Vision + SwiftUI, no Python runtime, no external model.

`avfoundation` `vision` `swiftui`

</td>
<td width="50%" valign="top">

### [Tamagotchi](https://github.com/DeMart1n/Tamagotchi)
`public` · Go

Terminal pet in Go. Small enough to read in one sitting, complete enough to actually play.

`tui` `go` `state-machine`

</td>
</tr>
</table>

---

## What I'm good at

<table>
<tr><td>

🔒 **Data isolation as an architectural decision** — multi-tenancy through custom managers and form mixins, applied consistently across models, views and forms. On the other project, every media consent path routes through a single gate with a per-upload audit snapshot. Three paths with three rules is how a leak happens.

</td></tr>
<tr><td>

📈 **Algorithms, not just CRUD** — repetition segmentation with Savitzky-Golay and bidirectional peak/valley detection, DTW over angular features instead of raw coordinates, detector parameters calibrated by per-template grid search. Production logged 6 reps for a video with 16; I hand-labeled 14 videos, found the cause, and dropped mean error from **5.1 to 1.3** reps.

</td></tr>
<tr><td>

🔎 **Debugging to root cause, with measurement** — staging eating the production queue because it shared Redis DB 0. A flaky N+1 test counting the profiler's own queries. A Celery container in silent crash-loop (exit 137, no traceback) because boot imported Ultralytics. None of it shows up in a stack trace.

</td></tr>
<tr><td>

🧪 **Tests that exercise the real system** — ~240 files with pytest and factory-boy, including a suite against real Postgres for when SQLite lies about database behavior. Ran the payment flow end to end with a live test key and caught three defects the gateway mock was hiding.

</td></tr>
</table>

---

## Stats

<div align="center">

<img height="165" src="https://github-readme-stats.vercel.app/api?username=DeMart1n&show_icons=true&hide_border=true&bg_color=0D1117&title_color=2EAD33&icon_color=2EAD33&text_color=c9d1d9&include_all_commits=true&count_private=true" alt="GitHub stats">
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=DeMart1n&layout=compact&hide_border=true&bg_color=0D1117&title_color=2EAD33&text_color=c9d1d9&langs_count=8" alt="Top languages">

<br><br>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=DeMart1n&bg_color=0D1117&color=c9d1d9&line=2EAD33&point=ffffff&area=true&hide_border=true" width="100%" alt="Contribution graph">

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/DeMart1n/DeMart1n/output/github-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/DeMart1n/DeMart1n/output/github-snake.svg">
  <img src="https://raw.githubusercontent.com/DeMart1n/DeMart1n/output/github-snake.svg" alt="Contribution snake">
</picture>

</div>

---

## How I work

> A reported bug is a symptom. Before editing, I find every caller and fix it where they all pass through.
>
> Contract changes (route, serializer, response shape) ship only after the edge cases are covered.
>
> I document decisions, not code: why each choice, what was rejected, what's still open.
>
> I'd rather delete code than add it. An abstraction with one use case is debt wearing architecture's clothes.

Clean Code, Clean Architecture, SOLID and Object Calisthenics as reference, not religion.

---

## Certifications

[![Ultralytics YOLO in Production](https://img.shields.io/badge/Ultralytics_YOLO_in_Production-100%25_·_Jul_2026-0B23A9?style=for-the-badge&logo=ultralytics&logoColor=white)](https://academy.ultralytics.com/courses/yolo-in-production/certificate/fa3abed9-5d4a-404e-b193-0d2ae9283142)

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2EAD33,50:0F5132,100:092E20&height=120&section=footer" width="100%" alt="">
