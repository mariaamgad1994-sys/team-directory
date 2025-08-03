# team-directory
import React, { useState, useEffect } from "react";
import "bootstrap/dist/css/bootstrap.min.css";
const initialMembers = [
  {
    name: "John Smith",
    role: "Frontend Developer",
    image:
      "https://www.google.com/imgres?q=%D8%B5%D9%88%D8%B1%20%D8%A7%D8%B4%D8%AE%D8%A7%D8%B5&imgurl=https%3A%2F%2Fpng.pngtree.com%2Fbackground%2F20240328%2Foriginal%2Fpngtree-young-handsome-man-smiling-to-you-real-people-young-man-eyes-picture-image_8278274.jpg&imgrefurl=https%3A%2F%2Far.pngtree.com%2Ffreebackground%2Fyoung-handsome-man-smiling-to-you-real-people-young-man-eyes-photo_8278274.html&docid=UojlLFhgY0KNhM&tbnid=YfUOXsc46ZhACM&vet=12ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECCMQAA..i&w=1200&h=800&hcb=2&ved=2ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECCMQAA",
  },
  {
    name: "Emily Johnson",
    role: "UI/UX Designer",
    image:
      "https://www.google.com/imgres?q=%D8%B5%D9%88%D8%B1%20%D8%A7%D8%B4%D8%AE%D8%A7%D8%B5&imgurl=https%3A%2F%2Fpng.pngtree.com%2Fthumb_back%2Ffw800%2Fbackground%2F20221214%2Fpngtree-student-male-portrait-at-campus-people-lifestyle-beautiful-photo-image_42943866.jpg&imgrefurl=https%3A%2F%2Far.pngtree.com%2Ffreebackground%2Fstudent-male-portrait-at-campus-people-lifestyle-beautiful-photo_13075177.html&docid=GfzjA_ziixeMCM&tbnid=FeXyjo_FUL05EM&vet=12ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECBsQAA..i&w=640&h=960&hcb=2&ved=2ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECBsQAA",
  },
  {
    name: "Michael Brown",
    role: "Project Manager",
    image:
      "https://www.google.com/imgres?q=%D8%B5%D9%88%D8%B1%20%D8%A7%D8%B4%D8%AE%D8%A7%D8%B5&imgurl=https%3A%2F%2Fthemes.jozoor.com%2Finvention%2Far%2Fphotography%2Fwp-content%2Fuploads%2F2014%2F06%2F6472122961_c6477930d1_b-460x460.jpg&imgrefurl=https%3A%2F%2Fthemes.jozoor.com%2Finvention%2Far%2Fphotography%2Fgalleries%2Fpeople%2F&docid=jXJPlXsycBTIwM&tbnid=QQwxuAufaGYSTM&vet=12ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECBoQAA..i&w=460&h=460&hcb=2&ved=2ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECBoQAA",
  },
  {
    name: "Sophia Davis",
    role: "Backend Developer",
    image:
      "https://www.google.com/imgres?q=%D8%B5%D9%88%D8%B1%20%D8%A7%D8%B4%D8%AE%D8%A7%D8%B5&imgurl=https%3A%2F%2Fpbs.twimg.com%2Fmedia%2FEkuFrIYWkAQsW-z%3Fformat%3Djpg%26name%3Dlarge&imgrefurl=https%3A%2F%2Fx.com%2Fmajdigood%2Fstatus%2F1318294311499423744&docid=rMom4Vtjc_6jtM&tbnid=R8T84jb2E7-fbM&vet=12ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECD4QAA..i&w=1750&h=1771&hcb=2&ved=2ahUKEwi-mayi0--OAxXh9LsIHQ-3NMcQM3oECD4QAA",
  },
];

function App() {
  const [members, setMembers] = useState(() => {
    const saved = localStorage.getItem("team");
    return saved ? JSON.parse(saved) : initialMembers;
  });

  const [search, setSearch] = useState("");
  const [newMember, setNewMember] = useState({ name: "", role: "", image: "" });
  const [showForm, setShowForm] = useState(false);

  useEffect(() => {
    localStorage.setItem("team", JSON.stringify(members));
  }, [members]);

  const handleAddMember = () => {
    if (!newMember.name || !newMember.role || !newMember.image) {
      alert("Please enter all required data");
      return;
    }

    setMembers([...members, newMember]);
    setNewMember({ name: "", role: "", image: "" });
    setShowForm(false);
  };

  const handleDelete = (index) => {
    if (window.confirm("are you sure remove the member ?")) {
      const updated = members.filter((_, i) => i !== index);
      setMembers(updated);
    }
  };

  const filteredMembers = members.filter(
    (member) =>
      member.name.toLowerCase().includes(search.toLowerCase()) ||
      member.role.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div className="container py-4">
      <h2 className="text-center mb-4">Team Directory</h2>

      <div className="row mb-3">
        <div className="col-md-8 mx-auto">
          <input
            type="text"
            placeholder="Search name or role"
            className="form-control"
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />
        </div>
      </div>

      <div className="text-center mb-4">
        <button
          className="btn btn-primary"
          onClick={() => setShowForm((prev) => !prev)}
        >
          {showForm ? "Close window" : "Add member"}
        </button>
      </div>

      {showForm && (
        <div className="row justify-content-center mb-4">
          <div className="col-md-3 mb-2">
            <input
              type="text"
              placeholder="Name"
              className="form-control"
              value={newMember.name}
              onChange={(e) =>
                setNewMember({ ...newMember, name: e.target.value })
              }
            />
          </div>
          <div className="col-md-3 mb-2">
            <input
              type="text"
              placeholder="Roule"
              className="form-control"
              value={newMember.role}
              onChange={(e) =>
                setNewMember({ ...newMember, role: e.target.value })
              }
            />
          </div>
          <div className="col-md-4 mb-2">
            <input
              type="text"
              placeholder="Image url"
              className="form-control"
              value={newMember.image}
              onChange={(e) =>
                setNewMember({ ...newMember, image: e.target.value })
              }
            />
          </div>
          <div className="col-md-2 mb-2">
            <button className="btn btn-success w-100" onClick={handleAddMember}>
              Save
            </button>
          </div>
        </div>
      )}

      <div className="row">
        {filteredMembers.length === 0 ? (
          <p className="text-center text-muted">لا يوجد أعضاء مطابقين للبحث</p>
        ) : (
          filteredMembers.map((member, index) => (
            <div className="col-md-4 mb-4" key={index}>
              <div className="card h-100 text-center">
                <img
                  src={member.image}
                  className="card-img-top"
                  alt={member.name}
                  style={{ height: "200px", objectFit: "cover" }}
                />
                <div className="card-body">
                  <h5 className="card-title">{member.name}</h5>
                  <p className="card-text">{member.role}</p>
                  <button
                    className="btn btn-danger"
                    onClick={() => handleDelete(index)}
                  >
                    Remove
                  </button>
                </div>
              </div>
            </div>
          ))
        )}
      </div>
    </div>
  );
}

export default App;
