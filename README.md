package com.example.lr17;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    // 1. ОБЪЯВЛЯЕМ ПЕРЕМЕННЫЕ ЗДЕСЬ (на уровне класса)
    // Тогда они будут видны во всех методах ниже.
    private TextView tvResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        // Ваш код Edge-to-Edge
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            androidx.core.graphics.Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        // 2. НАХОДИМ ЭЛЕМЕНТЫ
        tvResult = findViewById(R.id.tvResult);
        Button btnShowDialog = findViewById(R.id.btnShowDialog);
        Button btnClearData = findViewById(R.id.btnClearData);

        // 3. ОБРАБОТЧИКИ НАЖАТИЙ
        btnShowDialog.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                showQuestionDialog(); // Вызываем первый метод
            }
        });

        btnClearData.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                showConfirmationDialog(); // Вызываем второй метод
            }
        });
        
        // Убрали отсюда builder.show(), так как он не должен быть в onCreate!
    }

    // 4. ДОБАВЛЯЕМ НЕДОСТАЮЩИЙ МЕТОД ДЛЯ ПЕРВОГО ДИАЛОГА
    private void showQuestionDialog() {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Вопрос");
        builder.setMessage("Вы хотите продолжить?");

        builder.setPositiveButton("Да", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                tvResult.setText("Вы выбрали: Да");
            }
        });

        builder.setNegativeButton("Нет", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                tvResult.setText("Вы выбрали: Нет");
            }
        });

        builder.show();
    }

    // 5. МЕТОД ДЛЯ ВТОРОГО ДИАЛОГА (у вас он был, но я почистил код)
    private void showConfirmationDialog() {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Подтверждение");
        builder.setMessage("Очистить данные?");

        builder.setPositiveButton("Да", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                tvResult.setText("Данные очищены");
                Toast.makeText(MainActivity.this, "Данные удалены", Toast.LENGTH_SHORT).show();
            }
        });

        builder.setNegativeButton("Нет", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                dialog.dismiss();
            }
        });

        builder.setNeutralButton("Отмена", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                tvResult.setText("Действие отменено");
            }
        });

        builder.show();
    }
}
