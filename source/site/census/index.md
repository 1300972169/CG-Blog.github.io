---
title: 网站统计
date: 2022-09-15 21:30:00
comments: false
---
<!-- Include the library. -->
<script
  src="https://unpkg.com/github-calendar@latest/dist/github-calendar.min.js">
</script>

<!-- Optionally, include the theme (if you don't want to struggle to write the CSS) -->
<link
  rel="stylesheet"
  href="https://unpkg.com/github-calendar@latest/dist/github-calendar-responsive.css"
/>

<!-- Prepare a container for your calendar. -->
<div class="calendar">
    <!-- Loading stuff -->
    Loading the data just for you.
</div>

<script>
    GitHubCalendar(".calendar", "1300972169");

    // or enable responsive functionality:
    GitHubCalendar(".calendar", "1300972169", { responsive: true });
    GitHubCalendar(".calendar", "1300972169", { tooltips: true });
    // Use a proxy
    GitHubCalendar(".calendar", "1300972169", {
       proxy (username) {
         return fetch(`https://your-proxy.com/github?user=${username}`)
       }
    }).then(r => r.text())
</script>
