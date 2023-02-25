# How to booking.com API for developers
an example of how you can call the Booking.com API to retrieve hotel information and availability:

- Create an account on the Booking.com affiliate program website: https://affiliate.booking.com/
- Once you are approved as an affiliate, go to the API documentation page: https://developers.booking.com/api/index.html
- Follow the instructions to obtain your API credentials, which include an API key and a secret. You will need these credentials to authenticate your API requests.
- Use the curl command or a library such as axios or request in your preferred programming language to send API requests to the Booking.com API.

### Here's an example curl command to retrieve hotel information and availability:

```rust

curl -X GET \
  'https://distribution-xml.booking.com/json/getHotelAvailability?city_ids=-2601889&checkin=2023-04-01&checkout=2023-04-03&room1=A&apiKey=<your_api_key>&locale=en_US&currency=EUR' \
  -H 'Content-Type: application/json'
  ```
In this example, the getHotelAvailability API endpoint is used to retrieve hotel availability information for a specific city and date range. The city_ids parameter specifies the ID of the city you want to search for (in this case, the city ID for Amsterdam is used), and the checkin and checkout parameters specify the check-in and check-out dates. The room1 parameter specifies the number and type of rooms you want to search for (in this case, a single room type A is used). The apiKey parameter should be replaced with your own API key.

-- Parse the JSON response returned by the API and use the hotel information and availability data as needed in your application.
Note that the Booking.com API has rate limits and usage restrictions that you must follow. Additionally, you may need to obtain additional permissions or agreements from Booking.com in order to use their API in a commercial application like RoomRaccoon. Be sure to read the API documentation and terms of service carefully before integrating the Booking.com API into your application.

-- To create rooms for a property in the Booking.com API, you will need to use the OTA_HotelInvNotifRQ request message. This message allows you to create, update, and delete room availability for a property.

### Here's an example of how to use the OTA_HotelInvNotifRQ message to create rooms for a property:

Construct an XML request message that includes information about the property, room types, and room availability.
Here's an example XML message that creates a property with two room types:

```php

<OTA_HotelInvNotifRQ xmlns="http://www.opentravel.org/OTA/2003/05" Version="1.0" TimeStamp="2023-02-28T12:00:00" Target="Production">
  <SellableProducts HotelCode="123456">
    <SellableProduct InvCode="room1" InvType="room" Status="Available">
      <Description Name="Room for 4 persons" />
      <GuestRoom>
        <Room>
          <RoomType RoomTypeCode="4person" />
        </Room>
        <Occupancy MaxOccupancy="4" MinOccupancy="1" />
      </GuestRoom>
    </SellableProduct>
    <SellableProduct InvCode="room2" InvType="room" Status="Available">
      <Description Name="Room for 2 persons" />
      <GuestRoom>
        <Room>
          <RoomType RoomTypeCode="2person" />
        </Room>
        <Occupancy MaxOccupancy="2" MinOccupancy="1" />
      </GuestRoom>
    </SellableProduct>
  </SellableProducts>
</OTA_HotelInvNotifRQ>
```

In this example, the SellableProducts element defines the property with the ID 123456. The SellableProduct elements define two room types with the IDs room1 and room2, and the Description elements provide a name for each room type. The RoomType elements specify the type of room (in this case, a room for 4 persons and a room for 2 persons), and the Occupancy elements specify the maximum and minimum occupancy for each room type.

- Send the XML request message to the Booking.com API using an HTTP POST request. You will need to include your API credentials and a few additional headers in the request.
Here's an example of how to send the XML request message using the axios library in Node.js:

```javascript
const axios = require('axios');

const xml = `...` // The XML request message
const apikey = '...'; // Your Booking.com API key
const apisecret = '...'; // Your Booking.com API secret

const response = await axios.post('https://supply-xml.booking.com/hotels/OTA_HotelInvNotif', xml, {
  headers: {
    'Content-Type': 'application/xml',
    'Authorization': `Basic ${Buffer.from(`${apikey}:${apisecret}`).toString('base64')}`,
    'Accept-Encoding': 'gzip, deflate',
    'Accept': '*/*',
    'User-Agent': 'Mozilla/5.0',
  },
});
```
In this example, the axios.post method is used to send the XML request message to the Booking.com API. The headers parameter includes the necessary headers to authenticate the request and specify the message type.

- Check the response from the API to ensure that the rooms were created successfully.
If the rooms were created successfully, the response from the API should include a status code of 200 and a message indicating that the room availability was updated.

hoply it helps!


