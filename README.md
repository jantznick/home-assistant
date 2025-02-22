# home-assistant
Places to store my home assistant related code

## Team Tracking Script/Automation.
Script is a script used with [HA Team Tracker](https://github.com/vasqued2/ha-teamtracker) to respond to the question of when a sports team has a game on a day.
The assistant recognizes the intent of the question and runs the script which works in three parts:
1. Ask an LLM to give a team short code, league and sport from the given intent and return it as a basic string. That's the data the sport tracker needs, and it works great every time, by itself or in the whoe process. There is some variance in the return from the LLM, optimizing the prompt might help.
2. Chain the above response into a HA assistant conversation using a custom sentence automation([team-tracking-automation.yaml](https://github.com/jantznick/home-assistant/blob/main/team_tracking_automation.yaml)) that triggers an update entity call to the sports tracker with the updated team, league sport. I was able to get this going individually, and once or twice as part of the chain.
3. Feed the data from the sport tracker to chatgpt asking for a human sounding piece of text. Assuming the sport tracker data is updated, this works great every time as well.

Originally all steps were working as expected in a chain or individually, then step 2 suddenly stopped recognizing the custom sentence.
  - The step 2 sentence originally was 'update teamtracking updatable league {league} team {team} sport {sport}' and when it changed to 'update teamtracking updatable {league} {team} {sport}' it stopped working so maybe it's something to do with no space between the trigger slot words.
