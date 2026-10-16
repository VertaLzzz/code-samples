#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>
using namespace std

void calculateRegression(int** data, int m, double& a, double& b) {
    double sum_x = 0.0;
    double sum_y = 0.0;
    double sum_xy = 0.0;
    double sum_x2 = 0.0;
    double m_double = static_cast<double>(m); 

    for (int i = 0; i < m; ++i) {
        double x = static_cast<double>(data[0][i]);
        double y = static_cast<double>(data[1][i]);

        sum_x += x;
        sum_y += y;
        sum_xy += (x * y);
        sum_x2 += (x * x);
    }
    double denominator = (m_double * sum_x2) - (sum_x * sum_x);
    if (denominator == 0.0) {
        a = 0.0;
        b = sum_y / m_double;
    } else {
        a = ((m_double * sum_xy) - (sum_x * sum_y)) / denominator;
        b = (sum_y - (a * sum_x)) / m_double;
    }
}

int main(int argc, char* argv[]) {
    if (argc != 2) {
        cerr << "Ошибка: Не указано имя входного файла.\n";
        cerr << "Использование: " << argv[0] << " <имя_файла>\n";
        return 1;
    }

    string input_filename = argv[1];
    ifstream infile(input_filename);
    if (!infile.is_open()) {
        cerr << "Ошибка: Не удалось открыть файл '" << input_filename << "'\n";
        return 1;
    }

    int n, m;
    infile >> n >> m;

    if (n != 2) {
        cerr << "Ошибка: Количество строк (n) должно быть равно 2. Получено: " << n << "\n";
        infile.close();
        return 1;
    }

    if (m <= 0) {
        cerr << "Ошибка: Количество точек (m) должно быть больше 0.\n";
        infile.close();
        return 1;
    }

    int** data = new int*[n];
    for (int i = 0; i < n; ++i) {
        data[i] = new int[m];
    }

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            infile >> data[i][j];
        }
    }
    infile.close();

    double a = 0.0, b = 0.0;
    calculateRegression(data, m, a, b);

    string output_filename = "output.txt";
    ofstream outfile(output_filename);

    if (!outfile.is_open()) {
        cerr << "Ошибка: Не удалось создать выходной файл '" << output_filename << "'\n";
    } else {
        outfile << fixed << setprecision(4) << a << " " << b << "\n";
        outfile.close();
        cout << "Результат успешно записан в " << output_filename << "\n";
    }
    for (int i = 0; i < n; ++i) {
        delete[] data[i]; 
    }
    delete[] data;

    return 0;
}
