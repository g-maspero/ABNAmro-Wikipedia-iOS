# Hello ABN Amro!

Hi there! I hope you find my code fun to read and review. You can find some guidance for it in this README!

## Context
I started this challenge on Saturday night, and continued working on it during Sunday. So the whole development time for it was 1 ½ working days. I would have loved to spend more time on it, but had a pretty heavy week at my current job, and some personal affairs to take care of during the weekend. Nevertheless, you will find what I hope is a pretty thorough job. Given the time constraints, some things were left out of scope, which will be mentioned on the _Proposals for improvement_ section.

## Test App Architecture

### Architecture Choice
I have worked with many architecture patterns, and VIPER has to be one of the favourites for me, so I decided to go with that one for the test app. I fully understand that my codebase is an overkill for a simple `UITableView`, but the purpose of such overkill is to have it as a topic of technical debate during my next interview.
You will find that the folder structure is divided in two main folders: `Core` and `UserFlows`. The first one contains all classes that are used across all the application such as: base classes, networking,  UI components, error handling, etc. The latter folder contains all the user flows that exist in the app. For this case, there was only one screen, so you will find only one folder -`Home`- inside, which contains the VIPER stack for the home screen. The `Module` file for each user flow (in this case the `HomeModule`) is the one respomsible for building the VIPER stack and resolving dependencies.
Finally events are handled the old fashioned way, that is via delegates and completion handlers. I would love to discuss other alternatives, such ass reactive programming during our next encounter.

### Protocol Oriented Programming
Pretty much everything is protocolorised, using protocol inheritance as well, and all dependencies are injected in initializers, to allow for mocking and interaction testing.

### Testing
I gave it my best to have a pretty high code coverage with unit testing. You will find both interaction and state tests depending on the class under test. You can find the mocked dependencies on the `Mock` folders, which expose an interface with all the spies that might be of interest.

### Swift Package Manager
I went with Swift Package Manager for package management. The only package used in the application is Alamofire for HTTP requests.

## Proposals for improvement

Here are some opportunities to improve the codebase and fuctionality of our test app:
- Mocking classes for unit testing is boring and time consuming. Using a library that generates the mocked classes can be a good idea for saving time.
- Improve error handling: you will find that the error handling and what is shown to the user is pretty basic in this app. This can be improved from both a product and technical point of view.
- Latitude and longitude validation. This one is pretty important: right now there is next to no validation other than making sure we are using a `Double` for latitude and longitude. It would be a good idea to improve the validation, and to have some good error handling to make it clear to the user what is happening when there is a misuse of the text fields in the app.
- Further testing: code coverage can be improved by testing more classes and covering execution branches that might have been left out.
- Add UI testing.
- Having a template for creating user flows. I have found that it is super useful to have a template for whenever a new screen is needed. Not only does it make your life easier, but it also helps keep the architecture consistent across the codebase, specially when lots of different devs get their hands in the code.

## Known Issues

I'm not a fan of how the `LocationManager` is interacting with the `PlacesViewController` in the modified Wikipedia app. There was this issue where the `LocationManager` would override the "hand set" location with the device's current location, that happened whenever the app was closed and was then launched. I set a flag for that, so as to have the `PlacesViewController`not ask the `LocationManager` to start monitoring the device's location. The fix feels more like a workaround than a robust solution, but it was a conciouss decision that I took based on the time constraints explained previously.

## How to run it

Last but not least, here is how to run everything!
1. Open and run the modified Wikipedia app (instructions can be found in the [Wikipedia iOS Repo](https://github.com/wikimedia/wikipedia-ios#building-and-running)) in a simulator.
2. Open and run the test app in the same simulator.
3. Tap on any of the fetched locations, and the modified Wikipedia app will launch on that place.
4. You can enter a custom latitude and longitude in the text fields on the top of the screen, and upon tapping of the _Take me there_ button. you will again be presented with the Wikipedia app on said location.

## Conclusions

This is the first time I get asked to extend an existing productive app for a code challenge, and I found it super fun and interesting. It definitely mimics the real work one would encounter in our daily lives as iOS devs.
I would love to have the possibility of discussing my solution with you!
Cheers!