# Daily

Personal daily-summary dashboard. **Not** linked from samiprehn.github.io.

**Live:** https://samiprehn.github.io/daily/

## Sections

- **Header:** date, current time
- **Weather:** time-slot cards
  - Weekdays: 8am @ 92117, noon @ 92121 (with UV), 5pm @ 92117
  - Weekends: same slots all at 92117
  - Tonight's low at 92117
- **Sunset:** time, top viewpoint + grade, live sun-on-horizon scene, link to sd-sunset
- **Stargazing tonight:** top dark-sky site, score %, clear-dark hours, cloud %, moon phase + illumination, live moon SVG, link to stargaze
- **Farmers markets today:** markets open today with weather at their mid-hour
- **Weekend prep** (every day except Sunday):
  - Dog beaches Sat + Sun (high temp, wind, noon humidity)
  - Saturday and Sunday markets
  - Best stargazing night (Sat vs Sun)

## Stack

Single-file HTML, vanilla JS, Tailwind via CDN. No backend, no API keys.

- **Open-Meteo** for hourly + daily forecasts (temp, apparent_temp, wind, humidity, UV, weather code) at each ZIP/beach
- **NWS gridpoint API** for sunset cloud cover at each viewpoint and stargazing score per dark-sky site
- **TAF Cloudflare Worker** (`sd-sunset-taf.sami-prehn.workers.dev`) for layered cloud data
- **sunrise-sunset.org** for tonight's sunset time
- **Inline ephemeris** (suncalc-style port) for sun + moon altitude, illumination, phase

Logic is duplicated from `sd_sunset`, `stargaze`, `sd_farmers_markets`, and `sd_dog_beaches` so this site shows numbers consistent with each.
