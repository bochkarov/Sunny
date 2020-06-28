# Sunny
## An application to display the current weather in a given city.

The __MVC__ architecture is applied, the __Delegate__ pattern is used, error handling with the __Error__ protocol, __Auto Layout__. Request data from the __API__ using __URLSession__, processing a __JSON__ response using the __Codable__ protocol.

When you first run this application, you will be asked for access to determine your current location. The application will show you the current weather for your location if you approve the request. This function is implemented using __CoreLocation__.

<img width="300" alt="Screenshot 2020-06-28 at 12 44 54" src="https://user-images.githubusercontent.com/55511062/85945444-120a5780-b93e-11ea-9eaf-0964c741146c.png">

```swift
extension ViewController: CLLocationManagerDelegate {
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        guard let location = locations.last else { return }
        let latitude = location.coordinate.latitude
        let longitude = location.coordinate.longitude
        networkWeatherManager.fetchCurrentWeather(forRequestType: .coordinate(latitude: latitude, longitude: longitude))
    }
    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        print(error.localizedDescription)
    }
}
```
If you want to know the current weather in any city, you just need to enter the name of this city and perform __API__ request using _Search_ button.

<img width="300" alt="Screenshot 2020-06-28 at 14 49 11" src="https://user-images.githubusercontent.com/55511062/85948050-bf856700-b94e-11ea-9866-0e77fb0f0890.png">

```swift
func fetchCurrentWeather(forRequestType requestType: RequestType) {
        var urlString = ""
        switch requestType {
        case .cityName(let city):
            urlString = "https://api.openweathermap.org/data/2.5/weather?q=\(city)&appid=\(apiKey)&units=metric"
            
        case .coordinate(let latitude, let longitude):
            urlString = "https://api.openweathermap.org/data/2.5/weather?lat=\(latitude)&lon=\(longitude)&appid=\(apiKey)&units=metric"
        }
        performRequest(withURLString: urlString)
}
 ```
 
 You can also see the current temperature and _feels like_ temperature in a dark theme.
 
 <img width="300" alt="Screenshot 2020-06-28 at 15 00 00" src="https://user-images.githubusercontent.com/55511062/85948327-9e257a80-b950-11ea-9686-32c9484e12fb.png">
 
 
