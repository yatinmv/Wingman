# Wingman

Wingman is an adaptive dating app that helps users find compatible partners based on their characteristics. By learning more about the user through their inputs, the app can recommend profiles that have a higher chance of being a good match. To encourage conversations, the app generates an icebreaker question or joke from the matched partner's bio.

## Implementation

### Backend Functionality

The backend is a Flask application that stores user profiles in a database. Users can register, login, update their profiles, and swipe right or left on other users. The application retrieves and sends data to the database using SQLAlchemy and Pandas.

The API endpoints include:

| Method | Endpoint | Description |
| --- | --- | --- |
| POST | /register | Register a new user |
| POST | /login | Log in a user |
| POST | /logout | Log out a user |
| GET | /all-users | Retrieve all users |
| GET | /user/<user_id> | Retrieve a specific user |
| GET | /get-similar-users/<user_id> | Retrieve similar users based on a user's characteristics |
| GET | /get-ice-breakers/<user_id> | Retrieve icebreaker questions based on a user's characteristics |
| PUT | /update-user | Update a user's profile |
| POST | /add-swipe | Add a swipe to a user's profile |
| GET | /matches/<user_id> | Retrieve a user's matches |

### User Sign-up/Login/Logout

For user authentication, JWT (JSON Web Token) is used. A token is issued to users upon login or registration, and a valid token is required to access protected endpoints.

### Content-based Profile Recommendations

The backend uses K-Means clustering to find similar users based on their age, diet, drinks, and orientation. The features are encoded to numerical features using LabelEncoder and scaled using StandardScaler. The features are then clustered into three clusters using KMeans, and the cluster label for the user with the given ID is obtained using kmeans.predict(). Based on the user's orientation and sex, the code filters the DataFrame to find similar users with the same cluster label and returns a DataFrame of similar users.

### Icebreaker Recommendations

The backend uses Latent Dirichlet Allocation (LDA) to extract dominant topics from a user's bio. These topics are then passed along to the ice breaker generator module, which creates a prompt asking for three brief icebreakers based on those topics and then sends that prompt to the OpenAI API. The GPT-3.5 Turbo model was chosen due to its reliability. The generated icebreakers are returned as a list for use in the app. If the OpenAI API is unavailable or fails to generate icebreakers, a fallback message with three default icebreakers is returned.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
