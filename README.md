# econ3916-lab13-multivariate-ols# Multivariate OLS — What "Controlling For" Actually Does

## Objective
I used simulated data with a known truth to show what adding a control to a regression actually does, when it removes bias, and when it creates it.

## Methodology
- Simulated wages that depend on education and on an unobserved ability term, then ran a short regression that leaves ability out and a long regression that puts it in.
- Checked the omitted-variable-bias formula (gamma times delta) against the actual gap between the short regression's coefficient and the truth.
- Recovered the long regression's coefficient with Frisch-Waugh-Lovell: I stripped out the part of education that ability explains, did the same for wages, and regressed what was left of wages on what was left of education.
- Simulated a collider, a variable caused by both the treatment and the outcome when the two are unrelated, and compared the regression with and without it as a control.
- Simulated two nearly identical regressors and used the variance inflation factor to see what multicollinearity does to the coefficients and their standard errors.
- Fitted a regression with an interaction between experience and union membership, so the return to experience could differ between the two groups.
- Asked an AI to write a function that builds a specification table, revised my prompt once, and checked its coefficients and standard errors against my own regressions.

## Key Findings
- **Omitted variable bias:** with ability left out, the return to education came out at 5,126, about twice the true 2,500. With ability in, it was 2,546, close to the truth.
- **The bias formula works:** gamma times delta predicted a bias of 2,629, and the actual bias was 2,626.
- **Controlling for is partialling out:** the Frisch-Waugh-Lovell two-step gave exactly the same coefficient as the full regression, 2,546.4985.
- **A bad control creates an effect:** controlling for the collider turned a true effect of zero into an estimate of −0.596, with a p-value that printed as 0.000.
- **Multicollinearity inflates, but doesn't bias:** the standard errors were about 12 times larger than they would be without the collinearity, but the two coefficients still added up to 5.009 against a true 5.
- **Interactions let effects differ by group:** the regression recovered a return to a year of experience close to the true 900 for non-union workers and 500 for union members.
- **Checking the AI:** the AI's specification table only matched my own regressions after I told it which standard errors to use, so it was useful for writing the repetitive code but I still had to check every number.
