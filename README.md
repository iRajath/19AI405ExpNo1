# ExpNo 1 : Developing AI Agent with PEAS Description  

### Name: S Rajath
### Register Number/Staff Id: 212224240127  

---

### AIM:  
To find the PEAS description for the given AI problem and develop an AI agent.  

---

### Theory  

#### Medicine prescribing agent:  
Such this agent prescribes medicine for fever (greater than 98.5 degrees) which we consider here as unhealthy, by the user temperature input, and another environment is rooms in the hospital (two rooms). This agent has to consider two factors: one is room location and an unhealthy patient in a random room. The agent has to move from one room to another to check and treat the unhealthy person.  

The performance of the agent is calculated by incrementing performance and each time after treating in one room again it has to check another room so that the movement causes the agent to reduce its performance. Hence, agents prescribe medicine to unhealthy.  

---

### PEAS DESCRIPTION:  

| *Agent Type*              | *Performance*                         | *Environment*  | *Actuators*         | *Sensors*                       |
|------------------------------|------------------------------------------|------------------|-----------------------|------------------------------------|
| Medicine prescribing agent   | Treating unhealthy, agent movement      | Rooms, Patient   | Medicine, Treatment   | Location, Temperature of patient   |

---

### DESIGN STEPS  

*STEP 1: Identifying the input:*  
Temperature from patients, Location.  

*STEP 2: Identifying the output:*  
Prescribe medicine if the patient in a random has a fever.  

*STEP 3: Developing the PEAS description:*  
PEAS description is developed by the performance, environment, actuators, and sensors in an agent.  

*STEP 4: Implementing the AI agent:*  
Treat unhealthy patients in each room. And check for the unhealthy patients in random room.  

*STEP 5:*  
Measure the performance parameters: For each treatment performance incremented, for each movement performance decremented.

### PROGRAM

```py
import random

class MedicinePrescribingAgent:
    def _init_(self):
        self.performance = 0
        self.rooms = {
            "Room1": self.generate_patient(),
            "Room2": self.generate_patient()
        }

    def generate_patient(self):
        """Generate a patient with random temperature"""
        temperature = round(random.uniform(97.0, 102.0), 1)  # Random temp
        return {"temperature": temperature}

    def treat_patient(self, room, patient):
        """Check temperature and treat if unhealthy"""
        print(f"\nAgent in {room} | Patient Temp: {patient['temperature']} °F")

        if patient["temperature"] > 98.5:
            print("→ Patient has fever. Prescribing medicine...")
            self.performance += 1  # Successful treatment
        else:
            print("→ Patient is healthy. No medicine required.")

    def run(self):
        rooms_list = list(self.rooms.keys())

        for i in range(len(rooms_list)):
            room = rooms_list[i]
            patient = self.rooms[room]

            # Sense and treat
            self.treat_patient(room, patient)

            # Move to next room if exists
            if i < len(rooms_list) - 1:
                print(f"Agent moving from {room} to {rooms_list[i+1]}...")
                self.performance -= 1  # Movement cost

        print("\nFinal Performance Score:", self.performance)


# Run the agent
agent = MedicinePrescribingAgent()
agent.run()

```
### OUTPUT

![alt text](<output.jpg>)