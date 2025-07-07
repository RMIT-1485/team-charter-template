<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>RMIT MKTG1485 Team Charter Form</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/docx/7.7.0/docx.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #ffffff;
      padding: 40px;
      color: #222160;
    }
    h1, h2, h3 {
      color: #ba372a;
    }
    .rmit-header {
      display: flex;
      align-items: center;
      gap: 20px;
    }
    .form-section {
      margin-bottom: 30px;
    }
    label {
      display: block;
      font-weight: bold;
      margin: 10px 0 5px;
    }
    input, textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 8px;
    }
    button {
      padding: 12px 20px;
      background-color: #ba372a;
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="rmit-header">
    <img src="https://www.rmit.edu.au/content/dam/rmit/brand-identity/logo/RMIT-Logo-Colour-RGB.png" alt="RMIT Logo" height="60">
    <h1>MKTG1485 Team Charter</h1>
  </div>

  <form id="charterForm">
    <div class="form-section">
      <h2>1. Team Name</h2>
      <input type="text" name="teamName" placeholder="Team Name">
    </div>

    <div class="form-section">
      <h2>2. Team Members and Contact Info</h2>
      <textarea name="teamMembers" rows="6" placeholder="Name | Student ID | Contact Method (email, Teams, etc.)"></textarea>
    </div>

    <div class="form-section">
      <h2>3. Team Values</h2>
      <textarea name="teamValues" rows="4" placeholder="e.g. Respect, Honesty, Curiosity, Reliability"></textarea>
    </div>

    <div class="form-section">
      <h2>4. Communication Plan</h2>
      <textarea name="communication" rows="4" placeholder="Primary method, response time, check-in schedule"></textarea>
    </div>

    <div class="form-section">
      <h2>5. Roles and Responsibilities</h2>
      <textarea name="roles" rows="6" placeholder="Assign roles: Coordinator, Research Lead, Document Manager, etc."></textarea>
    </div>

    <div class="form-section">
      <h2>6. Decision-Making Process</h2>
      <textarea name="decision" rows="3" placeholder="e.g. Consensus, majority vote, etc."></textarea>
    </div>

    <div class="form-section">
      <h2>7. Conflict Resolution</h2>
      <textarea name="conflict" rows="3" placeholder="How you will handle disagreements or missed deadlines"></textarea>
    </div>

    <div class="form-section">
      <h2>8. Commitment Statement</h2>
      <textarea name="commitment" rows="5" placeholder="Signatures and agreement to team values"></textarea>
    </div>

    <button type="button" onclick="exportCharter()">Export as Word Document</button>
  </form>

  <script>
    async function exportCharter() {
      const form = document.getElementById('charterForm');
      const data = new FormData(form);

      const doc = new docx.Document({
        sections: [
          {
            properties: {},
            children: [
              new docx.Paragraph({ text: "MKTG1485 – Team Charter", heading: docx.HeadingLevel.HEADING_1 }),
              ...[...data.entries()].map(([label, value]) => [
                new docx.Paragraph({ text: label.replace(/([A-Z])/g, ' $1'), heading: docx.HeadingLevel.HEADING_2 }),
                new docx.Paragraph(value || " ")
              ]).flat()
            ]
          }
        ]
      });

      const blob = await docx.Packer.toBlob(doc);
      const link = document.createElement("a");
      link.href = URL.createObjectURL(blob);
      link.download = "Team_Charter_MKTG1485.docx";
      link.click();
    }
  </script>
</body>
</html>
