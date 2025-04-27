# Agent
"""
Main entry point for the AI Agent prototype.
"""

from core.brain import Brain
from utils.logger import Logger
from utils.config import ConfigManager

class AIAgent:
    def __init__(self):
        self.config = ConfigManager("config.yaml")
        self.logger = Logger(self.config.get("log_level", "INFO"))
        self.brain = Brain(self.config)

    def run(self):
        self.logger.log("AI Agent is starting up...")
        self.logger.log(f"Loaded configuration: {self.config.data}")
        try:
            while True:
                user_input = input("You: ")
                if user_input.lower() in ["exit", "quit"]:
                    self.logger.log("Shutting down AI Agent.")
                    print("Goodbye!")
                    break
                response = self.brain.process(user_input)
                print(f"AI Agent: {response}")
        except KeyboardInterrupt:
            self.logger.log("AI Agent terminated by user.")
            print("\nGoodbye!")

if __name__ == "__main__":
    agent = AIAgent()
    agent.run()# agent
