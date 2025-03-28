# Jenkins CI/CD Pipeline

##  1. Початкове налаштування системи

###  Оновлення системи
```bash
sudo apt update
```

### Встановлення Java і перевірка версії (необхідно для Jenkins)
```bash
sudo apt install -y openjdk-17-jre
java -version

```
[Скріншот](https://drive.google.com/file/d/1ZSCZdX9GGPjmYcj-QJP3sCUxyukuHw1M/view?usp=drive_link)

---

## 2. Встановлення Jenkins


### Додавання ключа Jenkins
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
```

###  Додавання репозиторію Jenkins
```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/" \
  | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```
 [Скріншот](https://drive.google.com/file/d/1QntSJNz_9LdiyXXvm6Ry0G-t4l8Jn62H/view?usp=drive_link)

### Оновлення пакетів
```bash
sudo apt-get update
```

### Встановлення Jenkins
```bash
sudo apt install -y jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
```
[Скріншот](https://drive.google.com/file/d/1kJ2-tPY5TvMiWvGpw36oOBVlep0bYvNC/view?usp=drive_link)

- Доступ до вебінтерфейсу Jenkins: ` http://192.168.0.193:8080 `
- Отримання початкового пароля адміністратора:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

##  3. Налаштування Jenkins через вебінтерфейс

### Початкове налаштування через браузер
1. Перейти за адресою: `http://192.168.0.193:8080`
2. Ввести початковий пароль адміністратора
3. Вибрати "Install suggested plugins"
4. Створити адміністратора (`iryna`)
5. Увійти в систему як `iryna`

### Налаштування pipeline
1. Увійти до Jenkins
2. Створити **Pipeline job** з назвою `ira-pipeline`
 [Скріншот](https://drive.google.com/file/d/1A92BHGbg91WEqlpf2fzcZcAAme1uWt-7/view?usp=drive_link)

3. Обрати джерело — Git: `https://github.com/Ir04ka7/Repo-for-Jenkins.git`
4. Jenkins сам знайде `Jenkinsfile`

---

##  4. Репозиторій з Jenkinsfile

- GitHub-репозиторій: [Repo-for-Jenkins](https://github.com/Ir04ka7/Repo-for-Jenkins)
- Файл `Jenkinsfile` включає стадії: Prepare, Build, Test

```groovy
pipeline {
    agent any

    environment {
        JENKINS_URL = "http://192.168.0.193:8080/"
    }

    stages {
        stage('Prepare') {
            steps {
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
                    sudo apt install -y nodejs
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'npm -v'
            }
        }
        stage('Test') {
            steps {
                sh 'echo JENKINS_URL: $JENKINS_URL'
            }
        }
    }
}
```
 [Скріншот](https://drive.google.com/file/d/1AkwDagX91oUiI-Qid-letlMHkopt_tPj/view?usp=drive_link)
---

##  5. Перевірка Jenkinsfile та запуск Pipeline

### Перевірка Jenkinsfile
```bash
java -jar jenkins-cli.jar -s http://192.168.0.193:8080/ \
  -auth iryna:<token> declarative-linter < Jenkinsfile
```

### Запуск та перегляд результатів
- [Pipeline виконує такі етапи](https://drive.google.com/file/d/19nlzfn6A05vHfJCfzL4Vm1fy1bwiDyx5/view?usp=drive_link):
  - ✅ [**Prepare**](https://drive.google.com/file/d/1hhsdp3cy5Ap46orjNSlyqZQVRpDXQ-mO/view?usp=drive_link): Встановлено Node.js 22
  - ✅ [**Build**](https://drive.google.com/file/d/1EviNSVac9VhkYaF5NILoLC3dHCWscxWL/view?usp=drive_link): Виведено версію `npm`
  - ✅ [**Test**](https://drive.google.com/file/d/1WFNOeggHUY6zHCbueGMe4ppEtzsRuLWV/view?usp=drive_link): Виведено `JENKINS_URL`

### Вебінтерфейс перегляду
- Використано плагін **Blue Ocean** для візуалізації етапів
- Альтернатива: **Stage View** на сторінці job'у

---

## [Всі скріншоти](https://drive.google.com/drive/folders/1teoSC-7K6cjo_m9wbjElJYVrVjv_oOZk?usp=drive_link)
- Скріншоти з Jenkins: всі етапи виконано успішно
- Jenkins URL: `http://192.168.0.193:8080/`
- GitHub: [Repo-for-Jenkins](https://github.com/Ir04ka7/Repo-for-Jenkins)

---

## Висновок
- Jenkins успішно встановлено на Ubuntu VM
- Початкове налаштування виконано через вебінтерфейс
- Створено pipeline job з репозиторієм GitHub
- Створено Jenkins pipeline з 3-ма стадіями: Prepare, Build, Test
- Node.js встановлюється під час виконання pipeline
- Jenkinsfile протестовано, валідація пройдена

