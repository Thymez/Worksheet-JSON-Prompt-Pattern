# Worksheet JSON Prompt Pattern

ใช้ไฟล์นี้เป็นคำสั่งกลางสำหรับส่งให้ ChatGPT หรือ AI Chat อื่นสร้างชุด Prompt ใบงานในรูปแบบ JSON มาตรฐานเดียวกันทุกครั้ง

## วิธีใช้

1. คัดลอกข้อความทั้งหมดในหัวข้อ **Prompt พร้อมใช้งาน**
2. แก้เฉพาะ `หัวข้อชุดใบงาน`, `ระดับชั้น` และ `รายละเอียดเพิ่มเติม`
3. ส่งข้อความให้แชทที่ต้องการใช้งาน
4. แชทต้องส่งกลับเป็น JSON Object เดียว หรือสร้างเป็นไฟล์ `.json` ให้ดาวน์โหลด

## Prompt พร้อมใช้งาน

```text
สร้างชุด Prompt ใบงานตามหัวข้อที่ฉันระบุ โดยส่งผลลัพธ์เป็น JSON ตามโครงสร้างที่กำหนดด้านล่างอย่างเคร่งครัด

กติกาสำคัญ:
1. ตอบเป็น JSON Object เดียวเท่านั้น
2. ห้ามใส่คำอธิบาย Markdown หรือข้อความอื่นนอก JSON
3. ห้ามใช้ comments, trailing commas, TBD, ... หรือ placeholder ในผลลัพธ์จริง
4. ใส่ Cover Prompt, Worksheet Prompt ทุกหน้า และ Answer Key Prompt ไว้ใน JSON เดียวกัน
5. prompts.worksheets ต้องมีจำนวนเท่ากับ worksheetPageCount
6. pageNumber ต้องเรียงตั้งแต่ 1 ถึง worksheetPageCount
7. totalPageCount และ pages ต้องเท่ากับ worksheetPageCount + 2
8. Cover ต้องเป็น 3000 x 3000 px, 300 DPI
9. Worksheet และ Answer Key ต้องเป็น 2550 x 3300 px, 300 DPI, portrait
10. tags ต้องมีจำนวน 6 รายการ
11. Prompt แต่ละหน้าต้องเขียนครบ พร้อมนำไปใช้สร้างภาพ ห้ามย่อ
12. ใช้ \n สำหรับแบ่งบรรทัดภายใน JSON string
13. ตั้ง downloadFileName ตาม collectionName โดยลบอักขระต้องห้าม < > : " / \ | ? *
14. ชื่อไฟล์ต้องลงท้ายด้วย .json เพียงครั้งเดียว
15. หากระบบสร้างไฟล์ได้ ให้บันทึกเป็น UTF-8 JSON และส่งลิงก์ดาวน์โหลด
16. หากสร้างไฟล์ไม่ได้ ให้แสดง JSON ใน fenced json code block เพียงก้อนเดียว
17. ตรวจสอบว่า JSON สามารถ parse ได้จริงก่อนส่ง
18. ห้ามส่ง Prompt, SEO Title, Description หรือ Metadata แยกออกเป็นหลายส่วน
19. subjectAreas ต้องมี exactly 3 ค่า และทุกค่าต้องตรงกับ SUBJECT AREAS ALLOWLIST ด้านล่างแบบตัวอักษรต่อตัวอักษร
20. tags ต้องมี exactly 6 ค่า และทุกค่าต้องตรงกับ TAGS ALLOWLIST ด้านล่างแบบตัวอักษรต่อตัวอักษร
21. ห้ามสร้างค่า dropdown ใหม่ ห้ามย่อคำ ห้ามเปลี่ยนเครื่องหมาย และห้ามใช้ชื่อกลุ่มที่ disabled
22. ก่อนส่ง ให้ตรวจสมาชิกทุกค่าใน subjectAreas และ tags เทียบกับ allowlist ทีละค่า หากไม่ตรงต้องเลือกค่าใหม่ที่ใกล้เคียงที่สุดจาก allowlist
23. description ต้องเป็นคำอธิบายขายสินค้าสำหรับ TPT ฉบับเต็ม และห้ามกล่าวถึง AI, ChatGPT, prompts หรือ generated content
24. description ต้องระบุว่าสินค้าคืออะไร เหมาะกับใคร มีอะไรบ้าง ทักษะที่ฝึก วิธีใช้ในชั้นเรียน การเตรียมของครู และข้อความเตือนให้ดู preview
25. ภายใน description ให้ใส่ตัวหนาด้วยรูปแบบ `**ข้อความ**` เพื่อให้ TPT JSON Uploader Extension แปลงเป็น Rich Text
26. ทำหัวข้อสำคัญทุกส่วนเป็นตัวหนา เช่น `**What’s Included**`, `**Skills Students Practice**`, `**Ways to Use This Resource**`, `**Teacher Preparation**` และ `**Answer Key**`
27. ในย่อหน้าเปิด ให้ทำตัวหนาเฉพาะวลีสำคัญหรือชื่อสินค้า 1 จุด ห้ามทำทั้งย่อหน้าเป็นตัวหนา และห้ามใช้ตัวหนามากเกินไป
28. ใช้ `*ข้อความ*` ได้เฉพาะข้อความเน้นแบบตัวเอียง และใช้บรรทัดที่ขึ้นต้นด้วย `- ` สำหรับ bullet list หรือ `1. ` สำหรับ numbered list
29. เครื่องหมาย `**`, `*`, `- ` และ `1. ` ต้องอยู่ภายใน JSON string ของ description เท่านั้น และต้องใช้ `\n` คั่นแต่ละย่อหน้าหรือรายการ
30. ตรวจสอบว่าเครื่องหมายตัวหนา `**` เปิดและปิดครบทุกคู่ ห้ามใช้ Markdown heading เช่น `#`, `##` หรือ `###` ภายใน description
31. taxCode ต้องเป็น `"Other Digital Goods - No Physical Media"` เท่านั้น ห้ามใช้ `"Digital Goods"` หรือค่าอื่น
32. grades ต้องเป็น array ที่มี 1–4 ค่าไม่ซ้ำกัน และทุกค่าต้องมาจาก GRADES ALLOWLIST เท่านั้น ต้องเก็บทุกระดับชั้นในช่วงที่ระบุ ห้ามเลือกเฉพาะชั้นสุดท้าย
33. teachingDuration ต้องมีค่าเดียวจาก TEACHING DURATION ALLOWLIST เท่านั้น ห้ามใช้ค่าว่าง ห้ามเขียนช่วงเวลาเอง และห้ามใส่คำอธิบายต่อท้าย
34. pages และ totalPageCount ต้องเป็น JSON number ไม่ใช่ string ส่วน price, licensePrice และ bundlePrice ต้องเป็น string
35. รูปแบบและลำดับชื่อ key ระดับบนสุดต้องตรงกับ JSON Structure ด้านล่าง ห้ามตัด key ห้ามเพิ่ม key และห้ามเปลี่ยนชนิดข้อมูล

GRADES ALLOWLIST — เลือก 1–4 ค่าเท่านั้น:
Preschool
Kindergarten
1st Grade
2nd Grade
3rd Grade
4th Grade
5th Grade
6th Grade
7th Grade
8th Grade
9th Grade
10th Grade
11th Grade
12th Grade
Higher Education
Adult Education
Not Grade Specific

ห้ามเลือก `Not Grade Specific` ร่วมกับค่า grade อื่น

TEACHING DURATION ALLOWLIST — เลือก exactly 1 ค่าเท่านั้น:
N/A
30 Minutes
40 Minutes
45 Minutes
50 Minutes
55 Minutes
1 Hour
90 Minutes
2 Hours
3 Hours
2 Days
3 Days
4 Days
1 Week
2 Weeks
3 Weeks
1 Month
2 Months
3 Months
1 Semester
1 Year
Lifelong Tool
Other

STRICT DROPDOWN VALIDATION:
- ใช้ allowlist ต่อไปนี้เป็นแหล่งข้อมูลเดียวสำหรับ subjectAreas และ tags
- ห้ามเดาค่าจากชื่อหัวข้อหรือชื่อหมวด
- ค่าใดไม่ปรากฏใน allowlist ห้ามใส่ใน JSON
- subjectAreas.length ต้องเท่ากับ 3
- tags.length ต้องเท่ากับ 6
- ค่าภายในแต่ละ array ต้องไม่ซ้ำกัน

SUBJECT AREAS ALLOWLIST — เลือก exactly 3 ค่าเท่านั้น:
Art History
Coloring Pages
Graphic Arts
Visual Arts
Other (Arts)
Alphabet
Balanced Literacy
Close Reading
Creative Writing
ELA Test Prep
Grammar
Handwriting
Informational Text
Library Skills
Literature
Novel Studies
Phonics & Phonological Awareness
Poetry
Reading
Reading Strategies
Science of Reading
Short Stories
Sight Words
Spelling
Vocabulary
Writing
Writing-Essays
Writing-Expository
Other (ELA)
Health
Algebra
Algebra 2
Applied Math
Arithmetic
Basic Operations
Calculus
Decimals
Financial Literacy
Fractions
Geometry
Graphing
Math Test Prep
Measurement
Mental Math
Money Math
Numbers
Order of Operations
Place Value
PreCalculus
Statistics
Telling Time
Other (Math)
Dance
Drama
Instrumental Music
Music
Music Composition
Vocal Music
Other (Performing Arts)
Physical Education
Anatomy
Archaeology
Astronomy
Basic Principles
Biology
Chemistry
Computer Science - Technology
Earth Sciences
Engineering
Environment
Family Consumer Sciences
Forensics
General Science
Instructional Technology
Marine Science
Physical Science
Physics
Robotics
Other (Science)
Character Education
Classroom Community
School Psychology
Social Emotional Learning
AAPI History
African History
Ancient History
Asian Studies
Australian History
Black History
British History
Business
Canadian History
Civics
Criminal Justice - Law
Economics
Elections - Voting
European History
Geography
Government
Latino and Hispanic Studies
Middle Ages
Native Americans
Psychology
Religion
U.S. History
World History
Other (Social Studies)
Speaking & Listening
American Sign Language
Arabic
Chinese
French
Gaeilge
German
Hebrew
Italian
Japanese
Latin
Portuguese
Russian
Spanish
Other (World Language)
For All Subjects
Not Subject Specific

ห้ามใช้ Subject Area headings เหล่านี้ เพราะเป็น disabled groups:
Art
English Language Arts
Math
Performing Arts
Science
Social Emotional
Social Studies
World Languages

TAGS ALLOWLIST — เลือก exactly 6 ค่าเท่านั้น:
Homeschool
Parents
Staff & Administrators
TPT Sellers
En español
En français
English (UK)
Advanced Placement (AP)
Early Intervention
GATE / Gifted and Talented
International Baccalaureate (IB)
Montessori
Bulletin Board Ideas
Posters
Word Walls
Clip Art
Classroom Forms
Elective Course Proposals
Grant Proposals
Professional Documents
School Nurse Documents
Student Council
Bell Ringers
Centers
Cultural Activities
DBQs
Escape Rooms
Games
Internet Activities
Laboratory
Literature Circles
Project-based Learning
Projects
Research
Scripts
Simulations
Songs
Webquests
Bibliographies
Guided Reading Books
Handouts
Interactive Notebooks
Scaffolded Notes
Printables
Assessment
Critical Thinking and Problem Solving
Study Guides
Study Skills
Test Preparation
Flash Cards
Graphic Organizers
Homework
Independent Work Packet
Movie Guides
Task Cards
Workbooks
Awards and Certificates
Classroom Management
Homeschool Curricula
Leadership Lessons
Lectures
Lessons
Outlines
Reflective Journals for Teachers
Rubrics
Syllabi
Teacher Manuals
Teacher Planners
Thematic Unit Plans
Tools for Common Core
Tools for Sellers
Unit Plans
Yearlong Curriculum
ESL, EFL, and ELL
Applied Behavior Analysis
Data
Life Skills
Neurodiversity
Screenings and Assessments
Social Skills
Visual Supports
Other (Special education)
Career and Technical Education
Child Care
Coaching
Cooking
Leadership
Occupational Therapy
Physical Therapy
Professional Development
Service Learning
Vocational Education
Other (Specialty)
AAC
Fluency and Stuttering
Language
Speech Articulation
Voice
Other (Speech therapy)
AAPI History Month
April Fools' Day
Arbor Day
Black History Month
Christmas-Chanukah-Kwanzaa
Cinco de Mayo
Day of the Dead / Dia de los Muertos
Diwali
Earth Day
Easter
Father's Day
Groundhog Day
Halloween
Hispanic Heritage Month
July 4/Independence Day
Juneteenth
Labor Day
Lunar New Year
Mardi Gras
Martin Luther King Day
Memorial Day
Mother's Day
New Year
Passover
Presidents' Day
Ramadan
St. Patrick's Day
Thanksgiving
Valentine's Day
Veterans Day
Women's History Month
Autumn
End of Year
Spring
Summer
Winter

ห้ามใช้ Tag headings เหล่านี้ เพราะเป็น disabled groups:
Audience
Language
Programs & Methods
Programs
Resource Type
Classroom Decor
Forms
Hands-on Activities
Instruction
Student Assessment
Student Practice
Teacher Tools
Supports
Special Education
Specialty
Speech Therapy
Theme
Holiday
Seasonal

หัวข้อชุดใบงาน:
[ใส่หัวข้อที่ต้องการ]

ระดับชั้น:
[ใส่ระดับชั้น]

จำนวนหน้าใบงาน:
[ระบุจำนวน หรือเขียนว่า "เลือกตามความเหมาะสม"]

รายละเอียดเพิ่มเติม:
[ใส่รายละเอียด หรือเขียนว่า "ให้เลือกตามความเหมาะสม"]

ใช้ JSON Structure นี้:

{
  "schemaVersion": "1.0",
  "downloadFileName": "ชื่อชุดใบงาน.json",
  "title": "SEO Title ความยาวไม่เกิน 80 ตัวอักษร",
  "collectionName": "ชื่อชุดใบงาน",
  "styleId": "STYLE-ID",
  "worksheetPageCount": 8,
  "totalPageCount": 10,
  "description": "**ชื่อหรือประโยชน์สำคัญของสินค้า** ตามด้วยคำอธิบายย่อหน้าเปิด\n\n**What’s Included**\n- รายการที่ 1\n- รายการที่ 2\n\n**Skills Students Practice**\n- ทักษะที่ 1\n- ทักษะที่ 2",
  "productType": "Printable Worksheets",
  "pages": 10,
  "grades": [
    "Kindergarten"
  ],
  "subjectAreas": [
    "Social Emotional Learning",
    "Character Education",
    "Classroom Community"
  ],
  "tags": [
    "Classroom Management",
    "Visual Supports",
    "Social Skills",
    "Life Skills",
    "Printables",
    "Independent Work Packet"
  ],
  "answerKey": "Included",
  "freeResource": false,
  "price": "4.50",
  "licensePrice": "3.38",
  "bundlePrice": "",
  "taxCode": "Other Digital Goods - No Physical Media",
  "copyright": "original",
  "active": false,
  "thumbnailsMode": "auto",
  "formats": [
    "PDF"
  ],
  "customCategories": [],
  "teachingDuration": "1 Hour",
  "pageSize": "US Letter portrait worksheets, square cover",
  "dpi": 300,
  "brand": "MoonPencil Studio",
  "coverStyle": "Bright high-impact TPT cover colors using color psychology, strong contrast, and marketable thumbnail hierarchy",
  "interiorVisualStyle": "Soft colored illustrations, minimal pastel color, mostly white low-ink printable interiors",
  "keywords": [
    "keyword 1",
    "keyword 2",
    "keyword 3",
    "keyword 4",
    "keyword 5",
    "keyword 6"
  ],
  "activityShuffleRunId": "TOPIC-FORMAT-0000",
  "answerPlacementRunId": "TOPIC-ANS-0000",
  "prompts": {
    "cover": {
      "pageType": "cover",
      "canvas": {
        "widthPx": 3000,
        "heightPx": 3000,
        "dpi": 300,
        "orientation": "square"
      },
      "prompt": "Cover Prompt ฉบับเต็ม"
    },
    "worksheets": [
      {
        "pageNumber": 1,
        "pageTitle": "ชื่อใบงานหน้า 1",
        "activityFormat": "รูปแบบกิจกรรม",
        "canvas": {
          "widthPx": 2550,
          "heightPx": 3300,
          "dpi": 300,
          "orientation": "portrait"
        },
        "prompt": "Worksheet Prompt หน้า 1 ฉบับเต็ม"
      }
    ],
    "answerKey": {
      "pageType": "answerKey",
      "canvas": {
        "widthPx": 2550,
        "heightPx": 3300,
        "dpi": 300,
        "orientation": "portrait"
      },
      "prompt": "Answer Key Prompt ฉบับเต็ม พร้อมคำตอบที่ตรงกับใบงานทุกหน้า"
    }
  }
}

ขยาย prompts.worksheets ให้ครบทุกหน้าตาม worksheetPageCount และแทนค่าตัวอย่างทั้งหมดด้วยข้อมูลจริงก่อนส่งผลลัพธ์
```

## สิ่งที่แชทต้องส่งกลับ

- JSON Object เดียวที่มีข้อมูลครบทุกส่วน
- ไฟล์ `.json` ตั้งชื่อตามชุดใบงาน หากแชทรองรับการสร้างไฟล์
- Cover Prompt จำนวน 1 รายการ
- Worksheet Prompt ครบตาม `worksheetPageCount`
- Answer Key Prompt จำนวน 1 รายการ
- จำนวน `pages` ถูกต้องตามสูตร `worksheetPageCount + 2`

## ตัวอย่างชื่อไฟล์

ชื่อชุดใบงาน:

```text
Self-Control Worksheets: Stop, Pause & Choose Smart Choices K-3
```

ชื่อไฟล์ JSON:

```text
Self-Control Worksheets - Stop, Pause & Choose Smart Choices K-3.json
```

