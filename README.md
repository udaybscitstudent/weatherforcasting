<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather for casting</title>
    <link rel="stylesheet" href="weather.css">
     </head>
<body>
    <div class="card">
        <div class="search">
            <input type="text" name="search" placeholder="enter city name" spellcheck="false">
            <button onclick="cityValue()"><img src="images/search.png"></button>
        </div>
        <div class="weather">
            <img src="images/rain.png" class="whether-icon">
            <h1 class="temp">22°c</h1>
            <h2 class="city">patna</h2>
            <div class="details">
                <div class="col">
                    <img src="images/humidity.png">
                    <div>
                        <p class="humidity">50%</p>
                        <p>humidity</p>
                    </div>
                </div><div class="col">
                    <img src="images/wind.png">
                    <div>
                        <p class="wind">15km/h</p>
                        <p>wind speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <script>
          const apiKey = "206641a86f149e329b1a3251be536964";
        const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q="
        
        // const searchBox = document.querySelector(".search input");
        const searchBox=  document.querySelector(".search input");
        const searchBtn = document.querySelector(".search button");
        const weatherIcon = document.querySelector(".whether-icon");

        console.log(searchBox);
        async function checkWeather(city){
            const response = await fetch(apiUrl+ city +`&appid=${apiKey}`);
            var data = await response.json();
            console.log(data);
            document.querySelector(".city").innerHTML = data.name;
            document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°c";
            document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
            document.querySelector(".wind").innerHTML = data.wind.speed + "km/h";

            if(data.weather[0].main == "Clouds"){
                weatherIcon.src= "images/clouds.png";
            }
            else if(data.weather[0].main == "Clear"){
                weatherIcon.src= "images/clear.png";
            }
            else if(data.weather[0].main == "Rain"){
                weatherIcon.src= "images/rain.png";
            }
            else if(data.weather[0].main == "Drizzle"){
                weatherIcon.src= "images/drizzle.png";
            }
            if(data.weather[0].main == "Mist"){
                weatherIcon.src= "images/mist.png";
            }



        }
        searchBtn.addEventListener("click",() => {
            checkWeather(searchBox.value);
        })
        checkWeather("patna");
    </script>
</body>
</html>
