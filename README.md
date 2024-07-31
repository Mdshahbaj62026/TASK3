# TASK3
JAVA


Creating a fully functional AI chatbot using Java involves integrating natural language processing (NLP) and machine learning techniques. In this example, we'll use the Stanford NLP library for NLP tasks and a simple machine learning model to handle user interactions.

Here's a simplified version of an AI chatbot:

Stanford NLP for Natural Language Processing: We'll use Stanford CoreNLP for tasks such as tokenization, part-of-speech tagging, and named entity recognition.

Simple Machine Learning Model: For this example, we'll use a rule-based approach rather than a full-fledged machine learning model due to the complexity and the need for a trained model.

Chatbot Class: This class will handle user interactions, process input using NLP, and generate responses.

Dependencies
To use the Stanford CoreNLP library, you need to download the library from the official website. Include the required JAR files in your project.

Chatbot.java
This class will handle user interactions and use Stanford CoreNLP for NLP tasks.

java

import edu.stanford.nlp.pipeline.*;
import edu.stanford.nlp.ling.*;
import edu.stanford.nlp.util.*;

import java.util.*;
import java.util.Properties;

public class Chatbot {

    private StanfordCoreNLP pipeline;

    public Chatbot() {
        Properties props = new Properties();
        props.setProperty("annotators", "tokenize,ssplit,pos,lemma,ner,parse");
        pipeline = new StanfordCoreNLP(props);
    }

    public String getResponse(String input) {
        Annotation annotation = new Annotation(input);
        pipeline.annotate(annotation);
        List<CoreMap> sentences = annotation.get(CoreAnnotations.SentencesAnnotation.class);

        StringBuilder response = new StringBuilder();
        for (CoreMap sentence : sentences) {
            for (CoreLabel token : sentence.get(CoreAnnotations.TokensAnnotation.class)) {
                String word = token.get(CoreAnnotations.TextAnnotation.class);
                String pos = token.get(CoreAnnotations.PartOfSpeechAnnotation.class);
                String ne = token.get(CoreAnnotations.NamedEntityTagAnnotation.class);
                response.append("Word: ").append(word).append(", POS: ").append(pos).append(", NE: ").append(ne).append("\n");
            }
        }

        // Simple rule-based responses
        if (input.toLowerCase().contains("hello")) {
            response.append("Hello! How can I help you today?");
        } else if (input.toLowerCase().contains("how are you")) {
            response.append("I'm just a program, but I'm functioning as expected!");
        } else if (input.toLowerCase().contains("bye")) {
            response.append("Goodbye! Have a great day!");
        } else {
            response.append("I'm sorry, I didn't understand that.");
        }

        return response.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Chatbot chatbot = new Chatbot();

        System.out.println("Chatbot: Hello! I am your chatbot. How can I assist you?");
        while (true) {
            System.out.print("You: ");
            String input = scanner.nextLine();
            if (input.equalsIgnoreCase("exit")) {
                System.out.println("Chatbot: Goodbye! Have a great day!");
                break;
            }
            String response = chatbot.getResponse(input);
            System.out.println("Chatbot: " + response);
        }

        scanner.close();
    }
}
Explanation
Dependencies: The code uses the Stanford CoreNLP library for NLP tasks. You need to download and include the Stanford CoreNLP JAR files in your project.

Chatbot Class:

Constructor: Initializes the Stanford CoreNLP pipeline with properties for tokenization, sentence splitting, part-of-speech tagging, lemmatization, named entity recognition, and parsing.
getResponse Method: Processes the input text, performs NLP tasks, and generates a response. For simplicity, we use a rule-based approach to generate responses based on keywords.
main Method: Handles user interaction, reads input from the console, and prints the chatbot's response. The loop continues until the user types "exit".
Running the Code
