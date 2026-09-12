<style scoped>
.code-editor {
  width: 700px;
  height: 340px;
  background-color: #1d1e22;
  box-shadow: 0px 4px 30px rgba(0, 0, 0, 0.5);
  border-radius: 8px;
  padding: 2px;
  z-index: 9999;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  @media (max-width: 600px) {
    width: 300px;
    height: 390px;
  }
}

.contoh-lembur {
  width: min(900px, 90%);
  max-height: 50vh;
  scrollbar-width: thin;
  scrollbar-color: #d90000 #f5f5f5;
  overflow-y: auto;
  margin: 30px auto;
  background: #ffffff;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
  z-index: 9999;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.judul {
  display: inline-block;
  background: #d90000;
  color: white;
  font-size: 24px;
  font-weight: bold;
  padding: 10px 25px;
  border-radius: 8px;
  margin-bottom: 25px;
}

.isi {
  color: #333;
  font-size: 17px;
  line-height: 1.7;
}

.isi p {
  margin: 0 0 18px;
  text-align: left;
}

.perhitungan {
  background: #f5f5f5;
  border-left: 5px solid #d90000;
  padding: 15px 20px;
  margin: 15px 0 25px;
  border-radius: 6px;
  font-size: 18px;
  @media (max-width: 500px) {
    font-size: 12px;
  }
}

.highlight {
  background: #fff1f1;
  padding: 15px 20px;
  margin: 15px 0 25px;
  border-radius: 8px;
  color: #d00000;
  @media (max-width: 500px) {
    font-size: 14px;
  }
}

.detail-lembur {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 20px;

  @media (max-width: 600px) {
    font-size: 11px;
  }
}

.detail-lembur div {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}

.detail-lembur span {
  text-align: right;
}

.total {
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  margin-top: 25px;
  padding: 18px 20px;
  height: 100px;
  background: #d90000;
  color: white;
  border-radius: 8px;
  font-size: 18px;
  flex-direction: column;
}

.total p,
strong {
  text-align: left;

  @media (max-width: 500px) {
    font-size: 11px;
  }
}
</style>

<template>
  <div class="contoh-lembur">
    <div class="judul">Contoh:</div>

    <div class="isi">
      <p>
        Gaji bulanan seorang karyawan adalah
        <strong>Rp4.000.000</strong>. Karyawan tersebut lembur selama
        <strong>3 jam</strong> di hari Kamis. Berapa uang lemburnya?
      </p>

      <p>
        Masukkan nominal gaji bulanan dan jam lembur, Saya akan menghitungkan
        simulasinya.
      </p>

      <p>Rumus menghitung upah perjam:</p>

      <div class="perhitungan">
        <strong>Rp4.000.000 × 1/173 = Rp23.121</strong>
      </div>

      <p>
        Lembur dilakukan pada hari kerja (Normal Day), rate yang berlaku adalah:
      </p>

      <div class="highlight">
        <strong>
          1,5 kali upah sejam pada jam pertama dan 2 kali upah sejam pada
          jam-jam berikutnya.
        </strong>
      </div>

      <div class="detail-lembur">
        <div>
          Uang lembur jam pertama
          <span>1,5 × Rp23.121 = <strong>Rp34.682</strong></span>
        </div>

        <div>
          Uang lembur jam kedua
          <span>2 × Rp23.121 = <strong>Rp46.242</strong></span>
        </div>

        <div>
          Uang lembur jam ketiga
          <span>2 × Rp23.121 = <strong>Rp46.242</strong></span>
        </div>
      </div>

      <div class="total">
        <span>Total upah lembur</span><br />
        <strong>Rp34.682 + Rp46.242 + Rp46.242 = Rp 48.557</strong>
      </div>
    </div>
  </div>
</template>
