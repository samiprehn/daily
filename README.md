# Daily

Personal daily-summary dashboard. **Not** linked from samiprehn.github.io.

**Live:** https://samiprehn.github.io/daily/

## Sections

- **Header:** date, current time
- **Weather:** time-slot cards (locations come from your localStorage Home/Work)
  - Weekdays: 8am @ Home, noon @ Work (with UV), 5pm @ Home
  - Weekends: all slots @ Home
  - Tonight's low at Home
- **Commute** (weekdays only): driving time with current traffic
  - Before noon: Home → Work
  - After noon: Work → Home
- **Sunset:** time, top viewpoint + grade, live sun-on-horizon scene, link to sd-sunset
- **Stargazing tonight:** top dark-sky site, score %, clear-dark hours, cloud %, moon phase + illumination, live moon SVG, link to stargaze
- **Farmers markets today:** markets open today with weather at their mid-hour
- **Weekend prep** (every day except Sunday):
  - Dog beaches Sat + Sun (high temp, wind, noon humidity)
  - Saturday and Sunday markets
  - Best stargazing night (Sat vs Sun)

## Stack

Single-file HTML, vanilla JS, Tailwind via CDN. No backend.

- **TomTom** for one-time geocoding of Home + Work addresses and for driving-traffic commute durations. The API key is in source but restricted in the TomTom dashboard to `samiprehn.github.io/*` so it only works when called from this site.
- **Home + Work addresses live in your browser's localStorage only.** Never uploaded to GitHub. First load shows a setup card asking for both addresses; afterwards an "edit locations" link at the bottom of the page lets you change them.
- **Open-Meteo** for hourly + daily forecasts (temp, apparent_temp, wind, humidity, UV, weather code) at Home/Work and each beach/market.
- **NWS gridpoint API** for sunset cloud cover at each viewpoint and stargazing score per dark-sky site.
- **TAF Cloudflare Worker** (`sd-sunset-taf.sami-prehn.workers.dev`) for layered cloud data.
- **sunrise-sunset.org** for tonight's sunset time.
- **Inline ephemeris** (suncalc-style port) for sun + moon altitude, illumination, phase.

Logic is duplicated from `sd_sunset`, `stargaze`, `sd_farmers_markets`, and `sd_dog_beaches` so this site shows numbers consistent with each.

## TomTom setup

1. Sign up at [developer.tomtom.com](https://developer.tomtom.com) (free, no credit card).
2. Get your default API key from the dashboard.
3. **Important:** edit the key → enable HTTP referrer restriction → add `https://samiprehn.github.io/*`. Save.
4. Drop the key into `TOMTOM_KEY` near the top of `index.html`.

The free tier gives 2,500 requests/day — way more than this dashboard uses.
