# 🕵️ Fraud Detection - Insurance Company project

An insurance company hires a team of data scientists to work as consultants in the fraud department. Currently, policies that are issued are monitored and any claims submitted are reviewed and evaluated, manually, to determine legitimacy and final approval for payment by the organization. 

**It is the role of the fraud team to determine which claims submitted should be approved and which should be should be rejected**.

Team's task is to answer the following question: **Are there particular trends in the groups of claims submitted that may be indicative of fraud?**

![insurance-analysis](img/thumbnail.jpg)

---

### Data preview

The finance department has provided them with data on all recent claims made by 1,000 customers. The data is not labeled; that is, there is no variable to tell us which of these claims are fraudulent or not.

Data provided is a table, which fields (columns) are:
- **case_id**: A unique identifier for each insurance case or claim. This field is likely a numerical value that differentiates one case from another.
- **income**: The annual income of the individual associated with the insurance case. This field is represented as a floating-point number and indicates the financial status of the policyholder.
- **age**: The age of the individual associated with the insurance case. This is an integer value representing how old the person is.
- **sex**: The gender of the individual associated with the insurance case. It is likely represented as 'M' for male and 'F' for female.
- **approval**: The status of the insurance claim. This field indicates whether the claim was "Approved" or "Denied."
- **fraud**: A categorical field indicating whether the insurance claim is under investigation for fraud. It might show values like "No" for non-fraudulent claims and "Under Review" or "Fraud" for those under suspicion.
- **claims**: The monetary amount of the insurance claims made by the individual. This field is a floating-point number representing the total value of the claims. ​

