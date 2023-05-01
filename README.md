# weather
import React, { useState } from 'react';
import axios from 'axios';

function App() {
  const [location, setLocation] = useState('');
  const [temperature, setTemperature] = useState('');
  const [humidity, setHumidity] = useState('');
  const [conditions, setConditions] = useState('');

  const handleSubmit = async (event) => {
    event.preventDefault();

    try {
      const response = await axios.get('/weather', {
        params: { location },
      });
      setTemperature(response.data.temperature);
      setHumidity(response.data.humidity);
      setConditions(response.data.conditions);
    } catch (error) {
      console.log(error);
    }
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={location}
          onChange={(event) => setLocation(event.target.value)}
        />
        <button type="submit">Get Weather</button>
      </form>
      {temperature && (
        <div>
          <p>Temperature: {temperature}</p>
          <p>Humidity: {humidity}</p>
          <p>Conditions: {conditions}</p>
        </div>
      )}
    </div>
  );
}

export default App;
