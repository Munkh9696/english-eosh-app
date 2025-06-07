# english-eosh-app
React Native ашигласан англи хэлний ЭЕШ жишээ тест апп
import React, { useState } from 'react';
import { View, Text, Button, TouchableOpacity, StyleSheet } from 'react-native';

const SampleTest = () => {
  const questions = [
    {
      question: 'Choose the correct word: "She _____ to school every day."',
      options: ['go', 'goes', 'going', 'gone'],
      correct: 'goes',
    },
  ];

  const [selected, setSelected] = useState(null);
  const [showResult, setShowResult] = useState(false);

  const checkAnswer = () => {
    setShowResult(true);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.question}>{questions[0].question}</Text>
      {questions[0].options.map((option) => (
        <TouchableOpacity
          key={option}
          style={[
            styles.option,
            selected === option && styles.selectedOption,
            showResult && option === questions[0].correct && styles.correctOption,
            showResult && selected === option && selected !== questions[0].correct && styles.wrongOption,
          ]}
          onPress={() => !showResult && setSelected(option)}
        >
          <Text style={styles.optionText}>{option}</Text>
        </TouchableOpacity>
      ))}
      <Button
        title="Check Answer"
        onPress={checkAnswer}
        disabled={selected === null || showResult}
      />
      {showResult && (
        <Text style={styles.resultText}>
          {selected === questions[0].correct ? 'Correct!' : `Wrong! Correct answer is "${questions[0].correct}"`}
        </Text>
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  container: { padding: 20 },
  question: { fontSize: 18, marginBottom: 20 },
  option: {
    padding: 10,
    marginVertical: 5,
    borderWidth: 1,
    borderColor: '#777',
    borderRadius: 5,
  },
  selectedOption: { backgroundColor: '#ddd' },
  correctOption: { backgroundColor: 'green', borderColor: 'green' },
  wrongOption: { backgroundColor: 'red', borderColor: 'red' },
  optionText: { fontSize: 16 },
  resultText: { marginTop: 20, fontSize: 18, fontWeight: 'bold' },
});

export default SampleTest;
