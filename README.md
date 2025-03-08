# 💫 About Me:
Hi 👋, I'm GOWTHAM P K<br>A passionate fullstack developer from India<br>🌱 I’m currently learning java (Spring Boot)<br><br>📫 How to reach me gowthampk004@gmail.com<br><br>


## 🌐 Socials:
[![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/gowthampk004) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](www.linkedin.com/in/gowtham-kumaravel-9226792a4) 

# 💻 Tech Stack:
![C](https://img.shields.io/badge/c-%2300599C.svg?style=for-the-badge&logo=c&logoColor=white) ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)  ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)  ![Canva](https://img.shields.io/badge/Canva-%2300C4CC.svg?style=for-the-badge&logo=Canva&logoColor=white) ![Figma](https://img.shields.io/badge/figma-%23F24E1E.svg?style=for-the-badge&logo=figma&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)![JAVA](https://img.shields.io/badge/Java-470137?style=for-the-badge&logo=Java&logoColor=#FF61F6)

name: Update Active Days Streak

on:
  schedule:
    - cron: '0 0 * * *'  # Runs daily at midnight UTC
  workflow_dispatch:  # Allows manual trigger

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Fetch Active Days
        run: |
          ACTIVE_DAYS=$(curl -s "https://api.github.com/users/gowthamkumaravel/events" | jq '.[].created_at' | cut -d'T' -f1 | sort -u | wc -l)
          echo "Active Days: $ACTIVE_DAYS"
          echo "ACTIVE_DAYS=$ACTIVE_DAYS" >> $GITHUB_ENV

      - name: Update README
        run: |
          sed -i "s|<!--ACTIVE_DAYS-->|$ACTIVE_DAYS|g" README.md

      - name: Commit and Push Changes
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"
          git add README.md
          git commit -m "Updated Active Days Counter"
          git push

