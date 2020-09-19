# TeslaAutoClimate with Microsoft Flow (Power Automate)
Based on an idea found at https://www.portiva.nl/nl/portiblog/microsoft-power-automate-tesla-api I decided to modify the Flow to add some missing parts.

You can download the Zip package and import it into your environment. The following variables have to be modified:
- username: This is your login for Tesla
- Password: Your Tesla password
- MinimalPower: Flow will not be executed if the SoC is below this value
- HeatorCoolingTime: How long should the cooling or heating run
- MinTemp: Heating will be run, if the outside temperature is below this value
- MaxTemp: Cooling will be run, if the inside temperature is above this value
- Temperature: The desired temperature inside the car

And last but not least: Edit the very first item, select the calendar and define the LookAhead time under "advanced". The LookAhead time should be the value as the HeatOrCoolingTime. The "Check agenda for calendar" should also be edited to match the subject you want.

What does the flow?
- Checks your calendar for upcoming events in the next xxx minutes (variable)
- If the subject of an upcoming event matches one of the entries in "Check agenda for calendar" the flow will continue
- The flow connects to the Tesla api (https://www.teslaapi.io/) and wakes up your car
- CHecks for the drive state (No heating or cooling necessary if you already drive)
- Checks if the State of charge is above "MinimalPower"
- Collects the outside and inside temperature from your car
- If inside temperature does not match "Temperature" the next steps will be executed
- If Outside temperature is below "MinTemp" heating will be run for the next xxx minutes and driver seat will be heated
- If Inside temperature is above "MaxTemp" cooling will be run for the next xxx minutes

If you have the Power Automate running on your mobile phone, you will receive notifications from the flow

Currently the user name and password for Tesla is stored in clear text inside the flow. This should be fixed in a later version
