window.onload = function () {
  shfaqHistorine();
};

function llogaritMesataren() {
  const nota1 = Number(document.getElementById("nota1").value);
  const nota2 = Number(document.getElementById("nota2").value);
  const nota3 = Number(document.getElementById("nota3").value);

  const mesatarja = ((nota1 + nota2 + nota3) / 3).toFixed(2);

  document.getElementById("rezultati").innerText =
    "Mesatarja: " + mesatarja;

  // Marrim historinë ekzistuese ose krijojmë bosh
  let historia = JSON.parse(localStorage.getItem("historiaMesatareve")) || [];

  // Shtojmë rezultatin e ri në fillim
  historia.unshift({
    nota1,
    nota2,
    nota3,
    mesatarja,
    data: new Date().toLocaleString()
  });

  // Mbajmë vetëm 10 të fundit
  if (historia.length > 10) {
    historia.pop();
  }

  // Ruajmë në localStorage
  localStorage.setItem(
    "historiaMesatareve",
    JSON.stringify(historia)
  );

  // Rifreskojmë listën në faqe
  shfaqHistorine();
}

function shfaqHistorine() {
  const lista = document.getElementById("historia");
  lista.innerHTML = "";

  const historia = JSON.parse(localStorage.getItem("historiaMesatareve")) || [];

  historia.forEach((item, index) => {
    const li = document.createElement("li");
    li.innerText =
      `${index + 1}. (${item.nota1}, ${item.nota2}, ${item.nota3}) → Mesatarja: ${item.mesatarja}`;
    lista.appendChild(li);
  });
}
