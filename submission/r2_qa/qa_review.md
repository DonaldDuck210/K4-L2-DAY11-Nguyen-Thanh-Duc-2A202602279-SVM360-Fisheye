# QA review · B4-dense

Mã khóa: 678F-E674

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_258420.jpg | ignore_region (ego_body) | R07 | Thân xe ego nhìn thấy ở mép dưới ảnh nhưng export không có polygon `ego_body`; cần vẽ theo phần thực sự nhìn thấy. |
| adasind_270517.jpg | ignore_region (ego_body) | R07 | Thân xe ego nhìn thấy ở mép dưới ảnh nhưng export không có polygon `ego_body`; cần vẽ theo phần thực sự nhìn thấy. |
| adasind_310008.jpg | ignore_region (ego_body) | R07 | Thân xe ego nhìn thấy ở mép dưới ảnh nhưng export không có polygon `ego_body`; cần vẽ theo phần thực sự nhìn thấy. |

Review theo ảnh và luật R07, không dùng teaching reference hoặc model để quyết định. Ghi ba finding `r2_qa`: `cell=L_only`, `what=STRUCTURE`, `rule_id=R07`, `why` để trống. Export đã khóa không bị sửa; chuyển các ca sang rework.

