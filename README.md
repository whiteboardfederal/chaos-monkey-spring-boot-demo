# Chaos Monkey Spring Boot Demo

This DEMO project is used to run a sample Chaos Experiment with spring boot. This application uses both [chaostoolkit](https://chaostoolkit.org/drivers/spring/) and [chaos-monkey-spring-boot](https://github.com/codecentric/chaos-monkey-spring-boot)

Once an experiment has ran, two files will be created: `journal.json` and `chaostoolkit.log`. 

The journal is one potenial output of a chaos engineering experiment. The objective of such journal is to collect all events that took place during the experiment’s run. The journal contains static information, such as the experiment that was run, as well as runtime entries.

In the event you need to investigate issues, logs will be appended to the `chaostoolkit.log` file. This file contains a lot of traces from the Chaos Toolkit core but also any extensions that used the toolkit’s logger.

## Install Maven/Gradle Dependencies

```
./mvnw install
```
```
./gradlew clean build
```

## Install Python
```
sudo apt-get install python3 python3-venv
```

## Configure Python and ChaosToolKit

Set virtual environment in python and install `chaostoolkit-spring`

```
python3 -m venv ~/.venvs/chaostk
source  ~/.venvs/chaostk/bin/activate
pip3 install -U chaostoolkit chaostoolkit-spring
```

## Start up Spring Boot
In a new terminal, start spring boot:
```
./mvnw spring-boot:run
```
```
./gradlew bootrun
```

## Run the Chaos Experiment
Run the experiment inside the python virtual env:
```
chaos run experiments/experiment.json
```

Output:

```
(chaostk)  chaostk > chaos run experiments.json
[2020-05-17 12:24:50 INFO] Validating the experiment's syntax
[2020-05-17 12:24:50 INFO] Experiment looks valid
[2020-05-17 12:24:50 INFO] Running experiment: Employee when database is down
[2020-05-17 12:24:50 INFO] Steady state hypothesis: Employee data is available
[2020-05-17 12:24:50 INFO] Probe: we-can-retrieve-employee-data
[2020-05-17 12:24:50 INFO] Steady state hypothesis is met!
[2020-05-17 12:24:50 INFO] Action: enable_chaosmonkey
[2020-05-17 12:24:50 INFO] Action: configure_assaults
[2020-05-17 12:24:50 INFO] Action: configure_repository_watcher
[2020-05-17 12:24:50 INFO] Steady state hypothesis: Employee data is available
[2020-05-17 12:24:50 INFO] Probe: we-can-retrieve-employee-data
[2020-05-17 12:24:50 INFO] Steady state hypothesis is met!
[2020-05-17 12:24:50 INFO] Let's rollback...
[2020-05-17 12:24:50 INFO] Rollback: disable_chaosmonkey
[2020-05-17 12:24:50 INFO] Action: disable_chaosmonkey
[2020-05-17 12:24:50 INFO] Experiment ended with status: completed

```

## REST endpoints
- `/actuator/chaosmonkey` - Chaos Monkey for Spring Boot
- `/employee/all` - Return employees from DB (H2)
