# Sunny
## An application to display the current weather in a given city.
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
If you want to know the current weather in a city, you just need to enter the name of this city.
