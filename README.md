# Jarlenny
Little Lemon Reservation
# 🍋 Little Lemon - Capstone Frontend Project

Este es el proyecto final (capstone) del curso de desarrollo Front-End.  
Consiste en una aplicación web desarrollada con React que permite a los usuarios **reservar mesas** en el restaurante ficticio **Little Lemon**.

## 🚀 Funcionalidades

- Formulario de reservas con validación de campos.
- Accesibilidad mejorada con etiquetas ARIA y etiquetas semánticas.
- Diseño responsive para móviles y escritorio.
- Pruebas unitarias con Jest y React Testing Library.
- Código organizado y versionado con Git y GitHub.

---

## 🛠️ Tecnologías usadas

- React
- HTML5 + CSS3
- JavaScript (ES6+)
- Jest + React Testing Library
- Git & GitHub

/src/components/BookingForm.js
import React, { useState } from 'react';

function BookingForm() {
  const [formData, setFormData] = useState({
    name: '',
    date: '',
    time: '',
    guests: 1,
    occasion: '',
  });

  const [submitted, setSubmitted] = useState(false);

  const handleChange = (e) => {
    const { name, value } = e.target;

    setFormData((prevData) => ({
      ...prevData,
      [name]: value,
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    // Validación básica
    if (
      formData.name &&
      formData.date &&
      formData.time &&
      formData.guests > 0 &&
      formData.occasion
    ) {
      console.log('Reserva enviada:', formData);
      setSubmitted(true);
    } else {
      alert('Por favor, completa todos los campos correctamente.');
    }
  };

  return (
    <form onSubmit={handleSubmit} aria-label="Formulario de Reserva">
      <div>
        <label htmlFor="name">Nombre completo:</label>
        <input
          type="text"
          id="name"
          name="name"
          required
          value={formData.name}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="date">Fecha:</label>
        <input
          type="date"
          id="date"
          name="date"
          required
          value={formData.date}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="time">Hora:</label>
        <select
          id="time"
          name="time"
          required
          value={formData.time}
          onChange={handleChange}
        >
          <option value="">Selecciona una hora</option>
          <option value="18:00">18:00</option>
          <option value="19:00">19:00</option>
          <option value="20:00">20:00</option>
        </select>
      </div>

      <div>
        <label htmlFor="guests">Número de comensales:</label>
        <input
          type="number"
          id="guests"
          name="guests"
          min="1"
          max="20"
          required
          value={formData.guests}
          onChange={handleChange}
        />
      </div>

      <div>
        <label htmlFor="occasion">Ocasión:</label>
        <select
          id="occasion"
          name="occasion"
          required
          value={formData.occasion}
          onChange={handleChange}
        >
          <option value="">Selecciona una ocasión</option>
          <option value="Cumpleaños">Cumpleaños</option>
          <option value="Aniversario">Aniversario</option>
          <option value="Otra">Otra</option>
        </select>
      </div>

      <button type="submit">Reservar</button>

      {submitted && <p>¡Reserva enviada con éxito!</p>}
    </form>
  );
}

export default BookingForm;


---

## 📦 Instalación y uso

1. Clona el repositorio:

```bash

npm install
git clone https://github.com/tu-usuario/little-lemon-reservations.git
cd little-lemon-reservations

import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import BookingForm from '../components/BookingForm';

test('muestra mensaje de éxito al enviar el formulario correctamente', () => {
  render(<BookingForm />);

  fireEvent.change(screen.getByLabelText(/nombre completo/i), {
    target: { value: 'Juan Pérez' },
  });
  fireEvent.change(screen.getByLabelText(/fecha/i), {
    target: { value: '2025-10-15' },
  });
  fireEvent.change(screen.getByLabelText(/hora/i), {
    target: { value: '18:00' },
  });
  fireEvent.change(screen.getByLabelText(/número de comensales/i), {
    target: { value: '4' },
  });
  fireEvent.change(screen.getByLabelText(/ocasión/i), {
    target: { value: 'Cumpleaños' },
  });

  fireEvent.click(screen.getByText(/reservar/i));

  expect(screen.getByText(/reserva enviada con éxito/i)).toBeInTheDocument();
});




