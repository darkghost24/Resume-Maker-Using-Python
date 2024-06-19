# Resume-Maker-Using-Python

"import tkinter as tk
from tkinter import ttk
from tkinter import messagebox


class ResumeMaker:
    def __init__(self, root):
        self.root = root
        self.root.title("Resume Maker")

        self.create_widgets()

    def create_widgets(self):
        # Personal Information
        personal_info_frame = ttk.LabelFrame(self.root, text="Personal Information")
        personal_info_frame.grid(row=0, column=0, padx=10, pady=10, sticky="ew")

        ttk.Label(personal_info_frame, text="Name:").grid(row=0, column=0, sticky="w")
        self.name_entry = ttk.Entry(personal_info_frame)
        self.name_entry.grid(row=0, column=1, sticky="ew")

        ttk.Label(personal_info_frame, text="Email:").grid(row=1, column=0, sticky="w")
        self.email_entry = ttk.Entry(personal_info_frame)
        self.email_entry.grid(row=1, column=1, sticky="ew")

        ttk.Label(personal_info_frame, text="Phone:").grid(row=2, column=0, sticky="w")
        self.phone_entry = ttk.Entry(personal_info_frame)
        self.phone_entry.grid(row=2, column=1, sticky="ew")

        ttk.Label(personal_info_frame, text="Address:").grid(row=3, column=0, sticky="w")
        self.address_entry = ttk.Entry(personal_info_frame)
        self.address_entry.grid(row=3, column=1, sticky="ew")

        # Education
        education_frame = ttk.LabelFrame(self.root, text="Education")
        education_frame.grid(row=1, column=0, padx=10, pady=10, sticky="ew")

        self.education_entries = []
        self.add_education_entry(education_frame)

        # Add Education Button
        add_education_button = ttk.Button(education_frame, text="Add Education",
                                          command=lambda: self.add_education_entry(education_frame))
        add_education_button.grid(row=len(self.education_entries) + 1, column=0, columnspan=2, pady=5)

        # Work Experience
        experience_frame = ttk.LabelFrame(self.root, text="Work Experience")
        experience_frame.grid(row=2, column=0, padx=10, pady=10, sticky="ew")

        self.experience_entries = []
        self.add_experience_entry(experience_frame)

        # Add Experience Button
        add_experience_button = ttk.Button(experience_frame, text="Add Experience",
                                           command=lambda: self.add_experience_entry(experience_frame))
        add_experience_button.grid(row=len(self.experience_entries) + 1, column=0, columnspan=2, pady=5)

        # Skills
        skills_frame = ttk.LabelFrame(self.root, text="Skills")
        skills_frame.grid(row=3, column=0, padx=10, pady=10, sticky="ew")

        self.skills_entries = []
        self.add_skill_entry(skills_frame)

        # Add Skill Button
        add_skill_button = ttk.Button(skills_frame, text="Add Skill",
                                      command=lambda: self.add_skill_entry(skills_frame))
        add_skill_button.grid(row=len(self.skills_entries) + 1, column=0, columnspan=2, pady=5)

        # Create Resume Button
        create_resume_button = ttk.Button(self.root, text="Create Resume", command=self.create_resume)
        create_resume_button.grid(row=4, column=0, padx=10, pady=10)

    def add_education_entry(self, frame):
        row = len(self.education_entries)
        degree_entry = ttk.Entry(frame)
        institution_entry = ttk.Entry(frame)
        year_entry = ttk.Entry(frame)

        degree_entry.grid(row=row, column=0, padx=5, pady=5, sticky="ew")
        institution_entry.grid(row=row, column=1, padx=5, pady=5, sticky="ew")
        year_entry.grid(row=row, column=2, padx=5, pady=5, sticky="ew")

        self.education_entries.append((degree_entry, institution_entry, year_entry))

    def add_experience_entry(self, frame):
        row = len(self.experience_entries)
        job_title_entry = ttk.Entry(frame)
        company_entry = ttk.Entry(frame)
        years_entry = ttk.Entry(frame)
        description_entry = ttk.Entry(frame)

        job_title_entry.grid(row=row, column=0, padx=5, pady=5, sticky="ew")
        company_entry.grid(row=row, column=1, padx=5, pady=5, sticky="ew")
        years_entry.grid(row=row, column=2, padx=5, pady=5, sticky="ew")
        description_entry.grid(row=row, column=3, padx=5, pady=5, sticky="ew")

        self.experience_entries.append((job_title_entry, company_entry, years_entry, description_entry))

    def add_skill_entry(self, frame):
        row = len(self.skills_entries)
        skill_entry = ttk.Entry(frame)
        skill_entry.grid(row=row, column=0, padx=5, pady=5, sticky="ew")

        self.skills_entries.append(skill_entry)

    def create_resume(self):
        name = self.name_entry.get()
        email = self.email_entry.get()
        phone = self.phone_entry.get()
        address = self.address_entry.get()

        education = []
        for degree_entry, institution_entry, year_entry in self.education_entries:
            degree = degree_entry.get()
            institution = institution_entry.get()
            year = year_entry.get()
            if degree and institution and year:
                education.append({"degree": degree, "institution": institution, "year": year})

        experience = []
        for job_title_entry, company_entry, years_entry, description_entry in self.experience_entries:
            job_title = job_title_entry.get()
            company = company_entry.get()
            years = years_entry.get()
            description = description_entry.get()
            if job_title and company and years and description:
                experience.append(
                    {"job_title": job_title, "company": company, "years": years, "description": description})

        skills = [skill_entry.get() for skill_entry in self.skills_entries if skill_entry.get()]

        with open("resume.txt", "w") as f:
            f.write("Resume\n")
            f.write("======\n\n")

            f.write("Personal Information\n")
            f.write("---------------------\n")
            f.write(f"Name: {name}\n")
            f.write(f"Email: {email}\n")
            f.write(f"Phone: {phone}\n")
            f.write(f"Address: {address}\n\n")

            f.write("Education\n")
            f.write("---------\n")
            for edu in education:
                f.write(f"{edu['degree']} from {edu['institution']} ({edu['year']})\n")
            f.write("\n")

            f.write("Work Experience\n")
            f.write("----------------\n")
            for exp in experience:
                f.write(f"{exp['job_title']} at {exp['company']} ({exp['years']})\n")
                f.write(f"Description: {exp['description']}\n\n")

            f.write("Skills\n")
            f.write("------\n")
            for skill in skills:
                f.write(f"- {skill}\n")
            f.write("\n")"
        


if __name__ == "__main__":
    root = tk.Tk()
    app = ResumeMaker(root)
    root.mainloop()
