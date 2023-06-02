# averageofgivennumbers
xml file-
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/numbersEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter numbers (separated by commas)" />

    <Button
        android:id="@+id/calculateButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/numbersEditText"
        android:layout_marginTop="16dp"
        android:text="Calculate" />

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/calculateButton"
        android:layout_marginTop="16dp"
        android:textSize="18sp"
        android:text="The average of the numbers will be displayed here." />

</RelativeLayout>

java file-

package com.example.averageofgivennos;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    private EditText numbersEditText;
    private Button calculateButton;
    private TextView resultTextView;

    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        numbersEditText = findViewById(R.id.numbersEditText);
        calculateButton = findViewById(R.id.calculateButton);
        resultTextView = findViewById(R.id.resultTextView);

        calculateButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String numbersString = numbersEditText.getText().toString();

                if (numbersString.isEmpty()) {
                    resultTextView.setText("Please enter numbers.");
                    return;
                }

                String[] numbersArray = numbersString.split(",");
                int sum = 0;
                int count = 0;

                for (String numberString : numbersArray) {
                    try {
                        int number = Integer.parseInt(numberString.trim());
                        sum += number;
                        count++;
                    } catch (NumberFormatException e) {
                        // Ignore non-numeric inputs
                    }
                }

                if (count > 0) {
                    double average = (double) sum / count;
                    resultTextView.setText("The average of the numbers is: " + average);
                } else {
                    resultTextView.setText("No valid numbers entered.");
                }
            }
        });
    }
}
