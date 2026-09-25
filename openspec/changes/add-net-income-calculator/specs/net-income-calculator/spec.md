# Spec Delta

## Purpose

Lets a Simples Nacional PJ turn the gross amount received in a month into the net amount left, showing every deduction that makes up the difference.

## ADDED Requirements

### Requirement: Default deductions
The page SHALL start with these deduction values: Simples Nacional 6% of gross, INSS R$ 180,00 (fixed), accounting fee R$ 297,00 (fixed).

#### Scenario: First visit
- **WHEN** the page is opened for the first time on a device
- **THEN** the deductions in use are 6%, R$ 180,00 and R$ 297,00
- **AND** the deduction inputs are hidden, with only the gross amount input visible

### Requirement: Gross amount input
The page SHALL accept the gross amount in Brazilian format (`.` thousands separator, `,` decimal separator) and SHALL focus that input on load, so the amount can be typed immediately.

#### Scenario: Typing a pt-BR amount
- **WHEN** the user types `28.084,65`
- **THEN** the page reads it as 28084.65

#### Scenario: Empty or invalid input
- **WHEN** the gross input is empty or not a number
- **THEN** no result values are shown (placeholder dashes), and no error dialog appears

### Requirement: Breakdown calculation
The page SHALL compute, and update as the user types without a submit button:
- Simples = gross × Simples rate, rounded to the cent (half up)
- Total deductions = Simples + INSS + accounting fee
- Net = gross − total deductions
- Deduction share = total deductions ÷ gross, as a percentage with one decimal place

All money values SHALL be displayed as BRL (`R$ 1.234,56`).

#### Scenario: Reference month
- **WHEN** gross is `28.084,65` with default deductions
- **THEN** Simples shows `R$ 1.685,08`, INSS `R$ 180,00`, accounting `R$ 297,00`
- **AND** total deductions shows `R$ 2.162,08`
- **AND** net shows `R$ 25.922,57`
- **AND** deduction share shows `7,7%`

#### Scenario: Gross smaller than fixed deductions
- **WHEN** gross is `300,00` with default deductions
- **THEN** net shows a negative value `-R$ 195,00` highlighted as a warning

### Requirement: Editable deductions
The page SHALL provide an "Editar valores" control that opens a drawer with inputs for Simples rate (%), INSS (R$) and accounting fee (R$). On wide screens the drawer SHALL slide in from the right edge; on phone widths it SHALL be a bottom sheet that slides up and can be dragged down to dismiss. It SHALL also close with "OK", a tap outside it, or Escape. Changing any of them SHALL recalculate immediately. Edited values SHALL persist on the same device across visits, and a "Restaurar padrão" control SHALL return all three to the defaults.

#### Scenario: One-off different fee
- **WHEN** the user opens the "Editar valores" drawer and sets the accounting fee to `350,00`
- **THEN** total and net recalculate using R$ 350,00

#### Scenario: Edited values survive a reload
- **WHEN** the user edits INSS to `200,00` and reloads the page
- **THEN** INSS in use is still R$ 200,00
- **AND** the page shows that custom values are active

#### Scenario: Restore defaults
- **WHEN** the user clicks "Restaurar padrão"
- **THEN** the deductions return to 6%, R$ 180,00 and R$ 297,00

### Requirement: Light and dark theme
The page SHALL offer a control that switches between light and dark themes. Without a saved choice it SHALL follow the system preference; a chosen theme SHALL persist on the same device.

#### Scenario: Switch to dark
- **WHEN** the user taps the theme control while in light theme
- **THEN** the page switches to dark theme
- **AND** after a reload it is still dark

### Requirement: Privacy and availability
The page SHALL run entirely in the browser with no network calls after load, and SHALL NOT store the gross amount. It SHALL be usable on phone and desktop widths and in light and dark mode.

#### Scenario: Gross not remembered
- **WHEN** the user types a gross amount and reloads
- **THEN** the gross input is empty again
