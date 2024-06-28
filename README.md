# Rest-Api-IP-Tracker
Rest-Api-IP-Tracker is a web application that leverages the IP Geolocation API by IPify to track and display the geographic location of any given IP address. This project also uses Leaflet, a leading open-source JavaScript library for mobile-friendly interactive maps, to visualize the geolocation data on a dynamic map. 


```markdown
 Features

- Fetches geolocation data for any IP address using IPify's API.
- Displays detailed location information including city, region, country, and ISP.
- Visualizes the geolocation on an interactive Leaflet map.
- Responsive design for a seamless experience across devices.



Technologies Used

- Frontend: HTML, CSS, JavaScript
- API: [IP Geolocation API by IPify](https://geo.ipify.org/)
- Map Visualization:** [Leaflet](https://leafletjs.com/)

 Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/kgabo71/Rest-Api-IP-Tracker.git
    cd Rest-Api-IP-Tracker
    ```

2. Open `index.html` in your web browser.

Usage

1. Enter an IP address into the search form.
2. Click the "Search" button.
3. View the geolocation information and the location on the map.

 Code Overview

 HTML

- `index.html`: The main HTML file containing the structure of the web page.

 CSS

- `style.css`: The CSS file for styling the web page.

 JavaScript

- `script.js`: The JavaScript file containing the functionality to fetch geolocation data and update the map and UI.

```javascript
/* JavaScript example code */
const search_form = document.querySelector(".header_form");

search_form.addEventListener("submit", (event) => {
    event.preventDefault();
    const value = document.querySelector("#search").value;
    search_Ip_Address(value);
});

async function search_Ip_Address(ip_address) {
    const api_key = "your_api_key_here";
    const request = await fetch(`https://geo.ipify.org/api/v2/country,city?apiKey=${api_key}&ipAddress=${ip_address}`);
    const response = await request.json();
    const { location, ip, isp } = response;
    update_ui(ip, location.city, location.timezone, isp);
    create_map(location.lat, location.lng, location.country, location.region);
}

function create_map(lat, lng, country, region) {
    const map = L.map('map').setView([lat, lng], 14);
    L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 20,
        attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);
    const my_icon = L.icon({
        iconUrl: '/images/icon-location.svg',
        iconSize: [40, 60],
        iconAnchor: [22, 94],
        popupAnchor: [-3, -76],
    });
    L.marker([lat, lng], { icon: my_icon }).addTo(map).bindPopup(`${region}, ${country}`).openPopup();
}

function update_ui(ip_address, location, timezone, isp) {
    document.querySelector(".address").textContent = ip_address;
    document.querySelector(".location").textContent = location;
    document.querySelector(".utc").textContent = 'UTC' + timezone;
    document.querySelector(".isp").textContent = isp;
}

const defaultIp = "29.44.89.169";
search_Ip_Address(defaultIp);
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- [IPify](https://geo.ipify.org/)
- [Leaflet](https://leafletjs.com/)
- [OpenStreetMap](https://www.openstreetmap.org/)

```

