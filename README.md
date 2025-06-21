<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Piano Settimanale Allenamento Calcio</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');
  body {
    margin: 0;
    background-color: #121212;
    color: #e0e0e0;
    font-family: 'Poppins', sans-serif;
  }
  h1 {
    text-align: center;
    margin: 1rem 0;
    font-weight: 600;
    color: #66bb6a;
    font-size: 2.5rem;
  }
  .day-container {
    margin: 1.5rem auto;
    max-width: 900px;
    padding: 1rem;
    border-radius: 12px;
    background: #1e1e1e;
    box-shadow: 0 0 20px #2e7d32aa;
  }
  .day-title {
    font-weight: 700;
    font-size: 2rem;
    color: #81c784;
    margin-bottom: 0.75rem;
    border-bottom: 2px solid #81c784;
    padding-bottom: 0.2rem;
  }
  .sessions {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .session {
    flex: 1 1 45%;
    background: #272727;
    border-radius: 10px;
    padding: 1rem;
    box-shadow: inset 0 0 15px #388e3c88;
    display: flex;
    flex-direction: column;
  }
  .session-header {
    font-weight: 600;
    font-size: 1.3rem;
    margin-bottom: 0.75rem;
    color: #a5d6a7;
    text-align: center;
    border-bottom: 1px solid #388e3c88;
    padding-bottom: 0.3rem;
  }
  .exercise {
    background: #333;
    margin-bottom: 0.8rem;
    border-radius: 8px;
    overflow: hidden;
    transition: max-height 0.4s ease;
  }
  .exercise-header {
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 0.5rem 1rem;
    user-select: none;
  }
  .exercise-header:hover {
    background: #3a7d44;
  }
  input[type="checkbox"] {
    margin-right: 1rem;
    transform: scale(1.2);
    cursor: pointer;
  }
  label {
    flex-grow: 1;
    font-weight: 500;
    font-size: 1rem;
    cursor: pointer;
  }
  .exercise-toggle-icon {
    width: 20px;
    height: 20px;
    fill: none;
    stroke: #a5d6a7;
    stroke-width: 2.5;
    transition: transform 0.3s ease;
  }
  .exercise.expanded .exercise-toggle-icon {
    transform: rotate(90deg);
  }
  .exercise-description {
    background: #2a2a2a;
    padding: 0.75rem 1.25rem;
    font-size: 0.9rem;
    line-height: 1.3;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.5s ease, padding 0.5s ease;
  }
  .exercise.expanded .exercise-description {
    max-height: 500px;
    padding: 0.75rem 1.25rem;
  }
  @media (max-width: 720px) {
    .sessions {
      flex-direction: column;
    }
    .session {
      flex: 1 1 100%;
      margin-bottom: 1rem;
    }
  }
</style>
</head>
<body>

<h1>Piano Settimanale Allenamento Calcio</h1>
<div id="schedule"></div>

<script>
  const workoutData = [
    {
      day: "Lunedì",
      sessions: [
        {
          title: "Mattina – Gambe + Core",
          exercises: [
            {name: "Riscaldamento 3’: skip, jumping jack, mobilità anche", description:"Esegui 3 minuti di riscaldamento con skip, jumping jack e mobilità delle anche per preparare il corpo."},
            {name: "Squat jump 3x12", description:"Esegui squat con salto esplosivo, 3 serie da 12 ripetizioni per potenziare gambe."},
            {name: "Affondi camminati 3x12/gamba", description:"Cammina facendo affondi alternati, 3 serie da 12 ripetizioni per gamba."},
            {name: "Glute bridge 3x15", description:"Sdraiato a terra, solleva i glutei, 3 serie da 15 per rinforzare i glutei."},
            {name: "Polpacci su gradino 3x20", description:"Sali su un gradino con le punte dei piedi, fai 3 serie da 20 per polpacci."},
            {name: "Plank frontale 3x40”", description:"Mantieni la posizione plank frontale per 40 secondi, 3 volte per rafforzare il core."},
            {name: "Crunch + leg raise 3x20", description:"Esegui 20 crunch e 20 sollevamenti gambe per 3 serie, per addominali."}
          ]
        },
        {
          title: "Pomeriggio – Tecnica palla + agilità",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching gambe", description:"3 minuti di riscaldamento con palleggi e stretching per gambe."},
            {name: "Conduzione palla tra coni 4x30”", description:"Dribbla la palla tra coni per 30 secondi, ripeti 4 volte."},
            {name: "Dribbling stretto 4x", description:"Esegui dribbling stretti 4 volte per migliorare controllo palla."},
            {name: "Stop + passaggi muro 4x15", description:"Ferma la palla e passa contro il muro, 4 serie da 15."},
            {name: "Scatti 10/20 m 5x", description:"Esegui 5 scatti da 10-20 metri per velocità."},
            {name: "Slalom con palla 4x", description:"Fai slalom con la palla tra ostacoli, 4 serie."}
          ]
        }
      ]
    },
    {
      day: "Martedì",
      sessions: [
        {
          title: "Mattina – Parte superiore",
          exercises: [
            {name: "Riscaldamento 3’: circonduzioni braccia + stretching spalle", description:"Riscalda con circonduzioni e stretching spalle per 3 minuti."},
            {name: "Push-up 4x15", description:"Esegui 4 serie da 15 flessioni."},
            {name: "Dips su sedia 3x12", description:"Usa una sedia per dips, 3 serie da 12."},
            {name: "Rematore (plank to row) 3x10", description:"Esercizio plank con rematore, 3 serie da 10."},
            {name: "Shoulder tap plank 3x30”", description:"Plank con tocco spalla per 30 secondi, 3 serie."},
            {name: "Russian twist 3x30”", description:"Esegui Russian twist per 30 secondi, 3 serie."}
          ]
        },
        {
          title: "Pomeriggio – Controllo + passaggi",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching", description:"Riscaldamento con palleggi e stretching gambe."},
            {name: "Passaggi muro corti e lunghi 4x20", description:"Passaggi contro il muro corti e lunghi, 4 serie da 20."},
            {name: "Stop orientato + tiro 4x5", description:"Stop orientato palla e tiro, 4 serie da 5."},
            {name: "Gioco posizione con coni (o libri)", description:"Esercizio tattico con coni o libri per posizionamento."},
            {name: "Visualizzazione movimenti 5-10’", description:"Visualizza mentalmente movimenti e tattiche per 5-10 minuti."}
          ]
        }
      ]
    },
    {
      day: "Mercoledì",
      sessions: [
        {
          title: "Mattina – Full body + esplosività",
          exercises: [
            {name: "Riscaldamento 3’: burpees lenti + stretching dinamico", description:"3 minuti di riscaldamento con burpees lenti e stretching dinamico."},
            {name: "Jump squat 12", description:"Esegui 12 jump squat per potenziare esplosività gambe."},
            {name: "Push-up esplosivi 10", description:"10 flessioni esplosive per forza parte superiore."},
            {name: "Burpees 10", description:"10 burpees per forza esplosiva e cardio."},
            {name: "Affondi saltati 10/gamba", description:"Affondi con salto, 10 ripetizioni per gamba."},
            {name: "Plank 45”", description:"Mantieni plank per 45 secondi per rafforzare core."}
          ]
        },
        {
          title: "Pomeriggio – Tiro + controllo",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching gambe", description:"3 minuti di riscaldamento con palleggi e stretching gambe."},
            {name: "Stop palla al volo 3x10", description:"Stop palla al volo, 3 serie da 10."},
            {name: "Tiro muro 4x10", description:"Tiri contro il muro, 4 serie da 10."},
            {name: "Tiro dopo dribbling 4x5/piede", description:"Tiri dopo dribbling, 4 serie da 5 per piede."},
            {name: "Cross + movimento inserimento", description:"Cross e movimenti offensivi per inserimento."}
          ]
        }
      ]
    },
    {
      day: "Giovedì",
      sessions: [
        {
          title: "Mattina – Core + mobilità",
          exercises: [
            {name: "Riscaldamento 3’: skip + stretching dinamico anche/schiena", description:"Riscaldamento con skip e stretching dinamico per anche e schiena."},
            {name: "Plank frontale 3x1’", description:"Plank frontale per 1 minuto, 3 serie."},
            {name: "Plank laterale 3x40”/lato", description:"Plank laterale per 40 secondi per lato, 3 serie."},
            {name: "Addominali alti/bassi 3x20", description:"Addominali alti e bassi, 3 serie da 20."},
            {name: "Hollow hold 3x30”", description:"Mantieni posizione hollow hold per 30 secondi, 3 serie."},
            {name: "Stretching statico 10’", description:"Stretching statico per 10 minuti per recupero."}
          ]
        },
        {
          title: "Pomeriggio – Velocità + agilità",
          exercises: [
            {name: "Riscaldamento 3’: corsa + mobilità", description:"3 minuti corsa leggera e mobilità articolare."},
            {name: "Ladder o slalom 5 giri", description:"Esercizio ladder o slalom per agilità, 5 giri."},
            {name: "Scatti con cambio direzione 4x5", description:"4 serie da 5 scatti con cambio direzione."},
            {name: "Frenate improvvise 4x10 m", description:"Frenate improvvise su 10 metri, 4 serie."},
            {name: "Reattività visiva (app o comandi vocali)", description:"Esercizi per migliorare reattività visiva."}
          ]
        }
      ]
    },
    {
      day: "Venerdì",
      sessions: [
        {
          title: "Mattina – Forza funzionale",
          exercises: [
            {name: "Riscaldamento 3’: jumping jack + mobilità", description:"Jumping jack e mobilità per 3 minuti."},
            {name: "Bulgarian split squat 3x10/gamba", description:"Squat bulgaro 3 serie da 10 ripetizioni per gamba."},
            {name: "Push-up + shoulder tap 3x15", description:"Flessioni con tocco spalla, 3 serie da 15."},
            {name: "Salti su gradino 3x10", description:"Salti su gradino, 3 serie da 10."},
            {name: "Plank dinamico + russian twist 3x40”", description:"Plank dinamico e russian twist per 40 secondi, 3 serie."},
            {name: "Circuito finale (burpees, squat, jumping jack, plank) 3 giri", description:"Esegui 3 giri di circuito con burpees, squat, jumping jack e plank."}
          ]
        },
        {
          title: "Pomeriggio – Tecnica + resistenza",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching", description:"Palleggi e stretching gambe per 3 minuti."},
            {name: "4 tocchi: controllo, dribbling, passaggio, stop 3x", description:"Esercizio 4 tocchi per 3 serie."},
            {name: "Corsa 20’ alternando palla ogni 5’", description:"Corsa di 20 minuti alternando la palla ogni 5 minuti."},
            {name: "Slalom + tiro 4x", description:"Slalom con palla e tiro, 4 serie."},
            {name: "Circuito calcio completo 3x", description:"Circuito completo calcio, 3 serie."}
          ]
        }
      ]
    },
    {
      day: "Sabato",
      sessions: [
        {
          title: "Recupero attivo",
          exercises: [
            {name: "Stretching + mobilità 15-20’", description:"15-20 minuti di stretching e mobilità articolare."},
            {name: "Camminata o bici leggera 30’", description:"Camminata o bici leggera per 30 minuti."},
            {name: "Palleggi liberi + tiri leggeri", description:"Palleggi e tiri leggeri a piacere."}
          ]
        }
      ]
    },
    {
      day: "Domenica",
      sessions: [
        {
          title: "Riposo completo",
          exercises: [
            {name: "Riposo totale", description:"Giornata dedicata al completo recupero senza allenamenti."}
          ]
        }
      ]
    }
  ];

  function createExercise(exercise, dayIndex, sessionIndex, exerciseIndex) {
    const exerciseDiv = document.createElement('div');
    exerciseDiv.classList.add('exercise');
    const id = `chk-${dayIndex}-${sessionIndex}-${exerciseIndex}`;

    const header = document.createElement('div');
    header.className = 'exercise-header';

    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.id = id;
    // Load state from localStorage
    const saved = localStorage.getItem(id);
    if (saved === 'true') checkbox.checked = true;

    checkbox.addEventListener('change', () => {
      localStorage.setItem(id, checkbox.checked);
    });

    const label = document.createElement('label');
    label.htmlFor = id;
    label.textContent = exercise.name;

    const arrowSvg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
    arrowSvg.setAttribute("viewBox", "0 0 24 24");
    arrowSvg.classList.add('exercise-toggle-icon');
    const polyline = document.createElementNS("http://www.w3.org/2000/svg", "polyline");
    polyline.setAttribute("points", "6 9 12 15 18 9");
    polyline.setAttribute("stroke-linecap", "round");
    polyline.setAttribute("stroke-linejoin", "round");
    arrowSvg.appendChild(polyline);

    header.appendChild(checkbox);
    header.appendChild(label);
    header.appendChild(arrowSvg);

    exerciseDiv.appendChild(header);

    const desc = document.createElement('div');
    desc.className = 'exercise-description';
    desc.textContent = exercise.description;

    exerciseDiv.appendChild(desc);

    header.addEventListener('click', e => {
      // Don't toggle when clicking checkbox
      if (e.target === checkbox) return;
      exerciseDiv.classList.toggle('expanded');
    });

    return exerciseDiv;
  }

  function createSession(session, dayIndex, sessionIndex) {
    const sessionDiv = document.createElement('div');
    sessionDiv.className = 'session';

    const title = document.createElement('div');
    title.className = 'session-header';
    title.textContent = session.title;
    sessionDiv.appendChild(title);

    session.exercises.forEach((ex, exIndex) => {
      sessionDiv.appendChild(createExercise(ex, dayIndex, sessionIndex, exIndex));
    });

    return sessionDiv;
  }

  function renderSchedule() {
    const container = document.getElementById('schedule');
    container.innerHTML = '';

    workoutData.forEach((day, dayIndex) => {
      const dayDiv = document.createElement('div');
      dayDiv.className = 'day-container';

      const dayTitle = document.createElement('div');
      dayTitle.className = 'day-title';
      dayTitle.textContent = day.day;
      dayDiv.appendChild(dayTitle);

      const sessionsDiv = document.createElement('div');
      sessionsDiv.className = 'sessions';

      day.sessions.forEach((session, sessionIndex) => {
        sessionsDiv.appendChild(createSession(session, dayIndex, sessionIndex));
      });

      dayDiv.appendChild(sessionsDiv);
      container.appendChild(dayDiv);
    });
  }

  renderSchedule();
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Piano Settimanale Allenamento Calcio</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');
  body {
    margin: 0;
    background-color: #121212;
    color: #e0e0e0;
    font-family: 'Poppins', sans-serif;
  }
  h1 {
    text-align: center;
    margin: 1rem 0;
    font-weight: 600;
    color: #66bb6a;
    font-size: 2.5rem;
  }
  .day-container {
    margin: 1.5rem auto;
    max-width: 900px;
    padding: 1rem;
    border-radius: 12px;
    background: #1e1e1e;
    box-shadow: 0 0 20px #2e7d32aa;
  }
  .day-title {
    font-weight: 700;
    font-size: 2rem;
    color: #81c784;
    margin-bottom: 0.75rem;
    border-bottom: 2px solid #81c784;
    padding-bottom: 0.2rem;
  }
  .sessions {
    display: flex;
    gap: 2rem;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .session {
    flex: 1 1 45%;
    background: #272727;
    border-radius: 10px;
    padding: 1rem;
    box-shadow: inset 0 0 15px #388e3c88;
    display: flex;
    flex-direction: column;
  }
  .session-header {
    font-weight: 600;
    font-size: 1.3rem;
    margin-bottom: 0.75rem;
    color: #a5d6a7;
    text-align: center;
    border-bottom: 1px solid #388e3c88;
    padding-bottom: 0.3rem;
  }
  .exercise {
    background: #333;
    margin-bottom: 0.8rem;
    border-radius: 8px;
    overflow: hidden;
    transition: max-height 0.4s ease;
  }
  .exercise-header {
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 0.5rem 1rem;
    user-select: none;
  }
  .exercise-header:hover {
    background: #3a7d44;
  }
  input[type="checkbox"] {
    margin-right: 1rem;
    transform: scale(1.2);
    cursor: pointer;
  }
  label {
    flex-grow: 1;
    font-weight: 500;
    font-size: 1rem;
    cursor: pointer;
  }
  .exercise-toggle-icon {
    width: 20px;
    height: 20px;
    fill: none;
    stroke: #a5d6a7;
    stroke-width: 2.5;
    transition: transform 0.3s ease;
  }
  .exercise.expanded .exercise-toggle-icon {
    transform: rotate(90deg);
  }
  .exercise-description {
    background: #2a2a2a;
    padding: 0.75rem 1.25rem;
    font-size: 0.9rem;
    line-height: 1.3;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.5s ease, padding 0.5s ease;
  }
  .exercise.expanded .exercise-description {
    max-height: 500px;
    padding: 0.75rem 1.25rem;
  }
  @media (max-width: 720px) {
    .sessions {
      flex-direction: column;
    }
    .session {
      flex: 1 1 100%;
      margin-bottom: 1rem;
    }
  }
</style>
</head>
<body>

<h1>Piano Settimanale Allenamento Calcio</h1>
<div id="schedule"></div>

<script>
  const workoutData = [
    {
      day: "Lunedì",
      sessions: [
        {
          title: "Mattina – Gambe + Core",
          exercises: [
            {name: "Riscaldamento 3’: skip, jumping jack, mobilità anche", description:"Esegui 3 minuti di riscaldamento con skip, jumping jack e mobilità delle anche per preparare il corpo."},
            {name: "Squat jump 3x12", description:"Esegui squat con salto esplosivo, 3 serie da 12 ripetizioni per potenziare gambe."},
            {name: "Affondi camminati 3x12/gamba", description:"Cammina facendo affondi alternati, 3 serie da 12 ripetizioni per gamba."},
            {name: "Glute bridge 3x15", description:"Sdraiato a terra, solleva i glutei, 3 serie da 15 per rinforzare i glutei."},
            {name: "Polpacci su gradino 3x20", description:"Sali su un gradino con le punte dei piedi, fai 3 serie da 20 per polpacci."},
            {name: "Plank frontale 3x40”", description:"Mantieni la posizione plank frontale per 40 secondi, 3 volte per rafforzare il core."},
            {name: "Crunch + leg raise 3x20", description:"Esegui 20 crunch e 20 sollevamenti gambe per 3 serie, per addominali."}
          ]
        },
        {
          title: "Pomeriggio – Tecnica palla + agilità",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching gambe", description:"3 minuti di riscaldamento con palleggi e stretching per gambe."},
            {name: "Conduzione palla tra coni 4x30”", description:"Dribbla la palla tra coni per 30 secondi, ripeti 4 volte."},
            {name: "Dribbling stretto 4x", description:"Esegui dribbling stretti 4 volte per migliorare controllo palla."},
            {name: "Stop + passaggi muro 4x15", description:"Ferma la palla e passa contro il muro, 4 serie da 15."},
            {name: "Scatti 10/20 m 5x", description:"Esegui 5 scatti da 10-20 metri per velocità."},
            {name: "Slalom con palla 4x", description:"Fai slalom con la palla tra ostacoli, 4 serie."}
          ]
        }
      ]
    },
    {
      day: "Martedì",
      sessions: [
        {
          title: "Mattina – Parte superiore",
          exercises: [
            {name: "Riscaldamento 3’: circonduzioni braccia + stretching spalle", description:"Riscalda con circonduzioni e stretching spalle per 3 minuti."},
            {name: "Push-up 4x15", description:"Esegui 4 serie da 15 flessioni."},
            {name: "Dips su sedia 3x12", description:"Usa una sedia per dips, 3 serie da 12."},
            {name: "Rematore (plank to row) 3x10", description:"Esercizio plank con rematore, 3 serie da 10."},
            {name: "Shoulder tap plank 3x30”", description:"Plank con tocco spalla per 30 secondi, 3 serie."},
            {name: "Russian twist 3x30”", description:"Esegui Russian twist per 30 secondi, 3 serie."}
          ]
        },
        {
          title: "Pomeriggio – Controllo + passaggi",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching", description:"Riscaldamento con palleggi e stretching gambe."},
            {name: "Passaggi muro corti e lunghi 4x20", description:"Passaggi contro il muro corti e lunghi, 4 serie da 20."},
            {name: "Stop orientato + tiro 4x5", description:"Stop orientato palla e tiro, 4 serie da 5."},
            {name: "Gioco posizione con coni (o libri)", description:"Esercizio tattico con coni o libri per posizionamento."},
            {name: "Visualizzazione movimenti 5-10’", description:"Visualizza mentalmente movimenti e tattiche per 5-10 minuti."}
          ]
        }
      ]
    },
    {
      day: "Mercoledì",
      sessions: [
        {
          title: "Mattina – Full body + esplosività",
          exercises: [
            {name: "Riscaldamento 3’: burpees lenti + stretching dinamico", description:"3 minuti di riscaldamento con burpees lenti e stretching dinamico."},
            {name: "Jump squat 12", description:"Esegui 12 jump squat per potenziare esplosività gambe."},
            {name: "Push-up esplosivi 10", description:"10 flessioni esplosive per forza parte superiore."},
            {name: "Burpees 10", description:"10 burpees per forza esplosiva e cardio."},
            {name: "Affondi saltati 10/gamba", description:"Affondi con salto, 10 ripetizioni per gamba."},
            {name: "Plank 45”", description:"Mantieni plank per 45 secondi per rafforzare core."}
          ]
        },
        {
          title: "Pomeriggio – Tiro + controllo",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching gambe", description:"3 minuti di riscaldamento con palleggi e stretching gambe."},
            {name: "Stop palla al volo 3x10", description:"Stop palla al volo, 3 serie da 10."},
            {name: "Tiro muro 4x10", description:"Tiri contro il muro, 4 serie da 10."},
            {name: "Tiro dopo dribbling 4x5/piede", description:"Tiri dopo dribbling, 4 serie da 5 per piede."},
            {name: "Cross + movimento inserimento", description:"Cross e movimenti offensivi per inserimento."}
          ]
        }
      ]
    },
    {
      day: "Giovedì",
      sessions: [
        {
          title: "Mattina – Core + mobilità",
          exercises: [
            {name: "Riscaldamento 3’: skip + stretching dinamico anche/schiena", description:"Riscaldamento con skip e stretching dinamico per anche e schiena."},
            {name: "Plank frontale 3x1’", description:"Plank frontale per 1 minuto, 3 serie."},
            {name: "Plank laterale 3x40”/lato", description:"Plank laterale per 40 secondi per lato, 3 serie."},
            {name: "Addominali alti/bassi 3x20", description:"Addominali alti e bassi, 3 serie da 20."},
            {name: "Hollow hold 3x30”", description:"Mantieni posizione hollow hold per 30 secondi, 3 serie."},
            {name: "Stretching statico 10’", description:"Stretching statico per 10 minuti per recupero."}
          ]
        },
        {
          title: "Pomeriggio – Velocità + agilità",
          exercises: [
            {name: "Riscaldamento 3’: corsa + mobilità", description:"3 minuti corsa leggera e mobilità articolare."},
            {name: "Ladder o slalom 5 giri", description:"Esercizio ladder o slalom per agilità, 5 giri."},
            {name: "Scatti con cambio direzione 4x5", description:"4 serie da 5 scatti con cambio direzione."},
            {name: "Frenate improvvise 4x10 m", description:"Frenate improvvise su 10 metri, 4 serie."},
            {name: "Reattività visiva (app o comandi vocali)", description:"Esercizi per migliorare reattività visiva."}
          ]
        }
      ]
    },
    {
      day: "Venerdì",
      sessions: [
        {
          title: "Mattina – Forza funzionale",
          exercises: [
            {name: "Riscaldamento 3’: jumping jack + mobilità", description:"Jumping jack e mobilità per 3 minuti."},
            {name: "Bulgarian split squat 3x10/gamba", description:"Squat bulgaro 3 serie da 10 ripetizioni per gamba."},
            {name: "Push-up + shoulder tap 3x15", description:"Flessioni con tocco spalla, 3 serie da 15."},
            {name: "Salti su gradino 3x10", description:"Salti su gradino, 3 serie da 10."},
            {name: "Plank dinamico + russian twist 3x40”", description:"Plank dinamico e russian twist per 40 secondi, 3 serie."},
            {name: "Circuito finale (burpees, squat, jumping jack, plank) 3 giri", description:"Esegui 3 giri di circuito con burpees, squat, jumping jack e plank."}
          ]
        },
        {
          title: "Pomeriggio – Tecnica + resistenza",
          exercises: [
            {name: "Riscaldamento 3’: palleggi + stretching", description:"Palleggi e stretching gambe per 3 minuti."},
            {name: "4 tocchi: controllo, dribbling, passaggio, stop 3x", description:"Esercizio 4 tocchi per 3 serie."},
            {name: "Corsa 20’ alternando palla ogni 5’", description:"Corsa di 20 minuti alternando la palla ogni 5 minuti."},
            {name: "Slalom + tiro 4x", description:"Slalom con palla e tiro, 4 serie."},
            {name: "Circuito calcio completo 3x", description:"Circuito completo calcio, 3 serie."}
          ]
        }
      ]
    },
    {
      day: "Sabato",
      sessions: [
        {
          title: "Recupero attivo",
          exercises: [
            {name: "Stretching + mobilità 15-20’", description:"15-20 minuti di stretching e mobilità articolare."},
            {name: "Camminata o bici leggera 30’", description:"Camminata o bici leggera per 30 minuti."},
            {name: "Palleggi liberi + tiri leggeri", description:"Palleggi e tiri leggeri a piacere."}
          ]
        }
      ]
    },
    {
      day: "Domenica",
      sessions: [
        {
          title: "Riposo completo",
          exercises: [
            {name: "Riposo totale", description:"Giornata dedicata al completo recupero senza allenamenti."}
          ]
        }
      ]
    }
  ];

  function createExercise(exercise, dayIndex, sessionIndex, exerciseIndex) {
    const exerciseDiv = document.createElement('div');
    exerciseDiv.classList.add('exercise');
    const id = `chk-${dayIndex}-${sessionIndex}-${exerciseIndex}`;

    const header = document.createElement('div');
    header.className = 'exercise-header';

    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.id = id;
    // Load state from localStorage
    const saved = localStorage.getItem(id);
    if (saved === 'true') checkbox.checked = true;

    checkbox.addEventListener('change', () => {
      localStorage.setItem(id, checkbox.checked);
    });

    const label = document.createElement('label');
    label.htmlFor = id;
    label.textContent = exercise.name;

    const arrowSvg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
    arrowSvg.setAttribute("viewBox", "0 0 24 24");
    arrowSvg.classList.add('exercise-toggle-icon');
    const polyline = document.createElementNS("http://www.w3.org/2000/svg", "polyline");
    polyline.setAttribute("points", "6 9 12 15 18 9");
    polyline.setAttribute("stroke-linecap", "round");
    polyline.setAttribute("stroke-linejoin", "round");
    arrowSvg.appendChild(polyline);

    header.appendChild(checkbox);
    header.appendChild(label);
    header.appendChild(arrowSvg);

    exerciseDiv.appendChild(header);

    const desc = document.createElement('div');
    desc.className = 'exercise-description';
    desc.textContent = exercise.description;

    exerciseDiv.appendChild(desc);

    header.addEventListener('click', e => {
      // Don't toggle when clicking checkbox
      if (e.target === checkbox) return;
      exerciseDiv.classList.toggle('expanded');
    });

    return exerciseDiv;
  }

  function createSession(session, dayIndex, sessionIndex) {
    const sessionDiv = document.createElement('div');
    sessionDiv.className = 'session';

    const title = document.createElement('div');
    title.className = 'session-header';
    title.textContent = session.title;
    sessionDiv.appendChild(title);

    session.exercises.forEach((ex, exIndex) => {
      sessionDiv.appendChild(createExercise(ex, dayIndex, sessionIndex, exIndex));
    });

    return sessionDiv;
  }

  function renderSchedule() {
    const container = document.getElementById('schedule');
    container.innerHTML = '';

    workoutData.forEach((day, dayIndex) => {
      const dayDiv = document.createElement('div');
      dayDiv.className = 'day-container';

      const dayTitle = document.createElement('div');
      dayTitle.className = 'day-title';
      dayTitle.textContent = day.day;
      dayDiv.appendChild(dayTitle);

      const sessionsDiv = document.createElement('div');
      sessionsDiv.className = 'sessions';

      day.sessions.forEach((session, sessionIndex) => {
        sessionsDiv.appendChild(createSession(session, dayIndex, sessionIndex));
      });

      dayDiv.appendChild(sessionsDiv);
      container.appendChild(dayDiv);
    });
  }

  renderSchedule();
</script>

</body>
</html>
