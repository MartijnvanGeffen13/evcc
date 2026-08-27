UP2DATE DEB files are in the release folder so you can directly download and install this addon

Hi everyone,

I recently submitted a pull request that introduces Dynamic MinSOC based on Solar Forecast, and I'd love your feedback and support.

👉 Pull Request: https://github.com/evcc-io/evcc/pull/32688

The feature is already available for testing on Ubuntu using the build attached to the pull request.

# Why is this needed?

Many EV owners face the same challenge, especially during the darker months of the year.

You arrive home from a trip with a low battery and plug in your vehicle. The question becomes:
How much should EVCC charge now, and how much capacity should be reserved for today's or tomorrow's solar production? If i fast charge how will i stop it when the sun starts shining.

After all, solar energy is typically the cheapest energy available.

Today, EVCC uses a static MinSOC value. While this works well in summer, it can be less efficient during winter:

- A high MinSOC may cause unnecessary grid charging when you arrive home.
- A low MinSOC may leave the vehicle insufficiently charged for an unexpected trip.
- Solar production later in the day may go unused because the battery is already full.
- Family members and other drivers often don't want to manually adjust charging settings after every trip.

# Introducing Dynamic MinSOC

### The concept is simple:

EVCC automatically adjusts the effective MinSOC based on the solar forecast.

This allows you to keep your vehicle in Solar mode while Dynamic MinSOC automatically determines how much fast charging is required.

## Example Scenarios: Vehicle returns with a low battery.
### ☀️ High Solar Forecast

- Significant solar production is expected.
- EVCC fast charges only to a low MinSOC level (for example 5% SOC).
- Maximum battery capacity remains available for solar charging.

### 🌤️ Medium Solar Forecast

- Moderate solar production is expected.
- EVCC fast charges to a medium MinSOC level (for example 40% SOC).
- The vehicle is asap ready for medium-distance trips while still reserving enough capacity for solar energy.

### ☁️ Low Solar Forecast
Little solar production is expected.
EVCC charges more aggressively from the grid to ensure the vehicle is ready when needed. (for example 80% SOC).
Only a small amount of battery capacity is reserved for available solar generation.

# The Result

A smarter balance between:

- Cost of Fuel
- Vehicle readiness
- Self-consumption of solar energy
- Reduced manual configuration
- Better charging efficiency throughout the year

## Key Benefits

✅ No need to manually adjust charging settings after every trip

✅ Optimizes charging behavior during winter and low-production periods

✅ Maximizes the use of available solar energy

✅ Works with existing weather forecast integrations

✅ Configurable solar thresholds (Low, Medium, High)

✅ Configurable MinSOC targets for each forecast level

✅ Existing MinSOC behavior remains supported and can override dynamic settings if required

✅ Configurable per vehicle, allowing adjustment for different battery sizes and driving patterns

# How You Can Help

If this functionality would be valuable for your setup, please:

- Test the build attached to the pull request
- Share your feedback and real-world experiences
- Upvote This discussion to help demonstrate community interest

Community feedback and adoption are important factors in determining which enhancements are prioritized, so every test and every vote helps.

Thank you for taking the time to review and test the feature. My goal is to make EV charging a little smarter, more automated, and more solar-friendly for everyone.

# Screenshots:

Extra configuration options in weather prediction settings:
<img width="492" height="524" alt="image" src="https://github.com/user-attachments/assets/6e6ee048-add1-4e5a-ad97-e65337b9474c" />


Car settings for overwrite or active setting:
<img width="843" height="521" alt="image" src="https://github.com/user-attachments/assets/0bbdef2d-2b59-4245-9cc7-401a76b4f7e1" />


--------------------

# evcc 🚘☀️

[![Build](https://github.com/evcc-io/evcc/actions/workflows/nightly.yml/badge.svg)](https://github.com/evcc-io/evcc/actions/workflows/nightly.yml)
[![Statuspage](https://img.shields.io/badge/status-evcc.io-green?color=brightgreen&link=https%3A%2F%2Fstatus.evcc.io)](https://status.evcc.io/)
[![Translation](https://hosted.weblate.org/widgets/evcc/-/evcc/svg-badge.svg)](https://hosted.weblate.org/engage/evcc/)
![Docker Pulls](https://img.shields.io/docker/pulls/evcc/evcc)
[![OSS hosting by cloudsmith](https://img.shields.io/badge/OSS%20hosting%20by-cloudsmith-blue?logo=cloudsmith)](https://cloudsmith.io/~evcc/packages/)
[![Latest Version](https://img.shields.io/github/release/evcc-io/evcc.svg)](https://github.com/evcc-io/evcc/releases)
<br/>
[![Built with Depot](https://depot.dev/badges/built-with-depot.svg)](https://depot.dev/?utm_source=evcc)

evcc is an extensible EV Charge Controller and home energy management system.

![Screenshot](assets/github/screenshot.webp)

Our goal is to provide local energy management, without relying on cloud services.
Featured in [PV Magazine](https://www.pv-magazine.de/2022/01/14/mit-open-source-lademanager-schnittstellen-zu-wallbox-und-photovoltaik-anlage-meistern/) and [c’t Magazin](https://www.youtube.com/watch?v=MoBpEXHMNjI).

## Features

- simple and clean user interface
- support for many [EV chargers](https://docs.evcc.io/en/docs/devices/chargers):
  - ABB, ABL, Alfen, Alphatec, Amperfied, Ampure, Audi, AUTEL, Autoaid, Bender, BMW, cFos, Charge Amps, Compleo, CUBOS, Cupra, Dadapower, DaheimLaden, Delta, E.ON Drive, E3/DC, Easee, Ebee, echarge, EcoHarmony, Edgetech, Elecq, eledio, Elli, EM2GO, EN+, enercab, Ensto, EntraTek, ESL, eSystems, Etrel, EVBox, Free2Move, Free2move eSolutions, Fronius, Garo, go-e, Hardy Barth, Heidelberg, Hesotec, Homecharge, Huawei, Innogy, INRO, Juice, Kathrein, KEBA, Kontron Solar, Kostal, KSE, LadeFoxx, LRT, Mennekes, NRGkick, OBO Bettermann, OpenEVSE, openWB, Optec, Orbis, PC Electric, Peblar, Phoenix Contact, Plugchoice, Porsche, Pracht, Pulsares, Pulsatrix, Qcells, Schneider, Schrack, SENEC, Siemens, Skoda, SMA, Smartfox, SolarEdge, Solax, Sonnen, Spelsberg, Stark in Strom, Sungrow, TechniSat, Tesla, Tigo, TinkerForge, Ubitricity, V2C Trydan, Vestel, Victron, Viridian EV, Volkswagen, Volt Time, Wallbe, wallbox, Walther Werke, Webasto, Weidmüller, Zaptec, ZJ Beny. [Read more.](https://docs.evcc.io/en/docs/devices/chargers)
  - **EEBus** support (Elli, PMCC)
  - **OCPP** support
  - **build-your-own:** Phoenix Contact (includes ESL Walli), EVSE DIN
  - **smart switches:** AVM, FRITZ!, Home Assistant, Homematic IP, HomeWizard, myStrom, Shelly, Tasmota, TP-Link. [Read more.](https://docs.evcc.io/en/docs/devices/smartswitches)
  - **heat pumps and electric heaters:** alpha innotec, Bosch, Buderus, Bösch, CTA All-In-One, Daikin, Elco, IDM, Junkers, Kermi, Lambda, my-PV, Nibe, Novelan, Roth, Stiebel Eltron, Tecalor, Vaillant, Viessmann, Wolf, Zewotherm. [Read more.](https://docs.evcc.io/en/docs/devices/heating)
- support for many [energy meters](https://docs.evcc.io/en/docs/devices/meters):
  - **solar inverters and battery systems:** A-Tronix, Acrel, Ads-tec, Alpha ESS, Ampere, Anker, APsystems, AVM, Axitec, BGEtech, Bosch, Bosswerk, Carlo Gavazzi, Deye, E3/DC, Eastron, Enphase, FENECON, FRITZ!, FoxESS, Fronius, Ginlong, go-e, GoodWe, Growatt, Homematic IP, HomeWizard, Hoymiles, Huawei, IAMMETER, IGEN Tech, Kostal, LG, Loxone, M-TEC, Marstek, myStrom, OpenEMS, Powerfox, Qcells, RCT, SAJ, SAX, SENEC, Senergy, Shelly, Siemens, Sigenergy, SMA, Smartfox, SofarSolar, Solaranzeige, SolarEdge, SolarMax, Solarwatt, Solax, Solinteng, Sonnen, St-ems, Steca, Sungrow, Sunsynk, Sunway, Tasmota, Tesla, TP-Link, VARTA, Victron, Wattsonic, Youless, ZCS Azzurro, Zendure. [Read more.](https://docs.evcc.io/en/docs/devices/meters)
  - **general energy meters:** A-Tronix, ABB, Acrel, Alpha ESS, Ampere, AVM, Axitec, Bernecker Engineering, BGEtech, Bosch, Carlo Gavazzi, cFos, Deye, DSMR, DZG, E3/DC, Eastron, Enphase, ESPHome, FENECON, FoxESS, FRITZ!, Fronius, Ginlong, go-e, GoodWe, Growatt, Homematic IP, HomeWizard, Huawei, IAMMETER, inepro, IOmeter, Janitza, KEBA, Kostal, LG, Loxone, M-TEC, mhendriks, my-PV, myStrom, OpenEMS, ORNO, P1Monitor, Powerfox, Qcells, RCT, Saia-Burgess Controls (SBC), SAJ, SAX, Schneider Electric, SENEC, Shelly, Siemens, Sigenergy, SMA, Smartfox, SofarSolar, Solaranzeige, SolarEdge, SolarMax, Solarwatt, Solax, Solinteng, Sonnen, St-ems, Sungrow, Sunsynk, Sunway, Tasmota, Tesla, Tibber, TQ, VARTA, Victron, Volkszähler, Wago, Wattsonic, Weidmüller, Youless, ZCS Azzurro, Zuidwijk. [Read more.](https://docs.evcc.io/en/docs/devices/meters)
  - **integrated systems**: SMA Sunny Home Manager and Energy Meter, KOSTAL Smart Energy Meter (KSEM, EMxx)
  - **sunspec**-compatible inverter or home battery devices
  - **mbmd**-compatible devices, see [volkszaehler/mbmd](https://github.com/volkszaehler/mbmd#supported-devices) for a complete list
- [vehicle](https://docs.evcc.io/en/docs/devices/vehicles) integrations (state of charge, remote charge, battery and preconditioning status):
  - Aiways, Audi, BMW, Citroën, Dacia, DS, Fiat, Ford, Genesis, Hyundai, Jeep, Kia, Mercedes-Benz, MG, Mini, Nissan, NIU, Opel, Peugeot, Polestar, Renault, Seat, Skoda, Smart, Subaru, Tesla, Toyota, Volkswagen, Volvo, Zero Motorcycles. [Read more.](https://docs.evcc.io/en/docs/devices/vehicles)
  - **services:** OVMS, Tronity, evNotify, ioBroker.bmw, mg2mqtt, mz2mqtt, TeslaLogger, TeslaMate, Tessi, volvo2mqtt
- [plugins](https://docs.evcc.io/en/docs/devices/plugins) for integrating with any charger, smartswitch, heatpump, electric heater, meter, solar- / battery-inverter or vehicle:
  - Modbus, HTTP, MQTT, JavaScript, WebSocket, Go and shell scripts
- status [notifications](https://docs.evcc.io/en/docs/reference/configuration/messaging) using [Telegram](https://telegram.org), [PushOver](https://pushover.net) and [many more](https://shoutrrr.nickfedor.com/)
- logging using [InfluxDB](https://www.influxdata.com) and [Grafana](https://grafana.com/grafana/)
- [REST](https://docs.evcc.io/en/docs/integrations/rest-api) and [MQTT](https://docs.evcc.io/en/docs/integrations/mqtt-api) APIs for integration with home automation systems
- Add-ons for [Home Assistant](https://docs.evcc.io/en/docs/integrations/home-assistant) and [openHAB](https://www.openhab.org/addons/bindings/evcc) (not maintained by the evcc core team)

## Getting Started

You'll find everything you need in our [documentation](https://docs.evcc.io/en/).

## Contributing

Technical details on how to contribute, how to add translations and how to build evcc from source can be found [here](CONTRIBUTING.md).

[![Weblate Hosted](https://hosted.weblate.org/widgets/evcc/-/evcc/287x66-grey.png)](https://hosted.weblate.org/engage/evcc/)

## Sponsorship

<img src="assets/github/evcc-gopher.png" align="right" width="150" />

evcc believes in open source software. We're committed to provide best in class EV charging experience.
Maintaining evcc consumes time and effort. With the vast amount of different devices to support, we depend on community and vendor support to keep evcc alive.

While evcc is open source, we would also like to encourage vendors to provide open source hardware devices, public documentation and support open source projects like ours that provide additional value to otherwise closed hardware. Where this is not the case, evcc requires "sponsor token" to finance ongoing development and support of evcc.

Learn more about our [sponsorship model](https://docs.evcc.io/en/docs/sponsorship).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

For additional license information regarding fonts, icons, and other assets, please see the [LICENSES](LICENSES/) folder.

**Note:** All sponsor-required components are excluded from the MIT License.
See file license header for details.
If you want to use them in your own project, one evcc sponsorship token is required per evcc instance.
Custom licensing agreements are available - please [contact us](mailto:info@evcc.io) to discuss your specific requirements.
